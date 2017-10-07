---
title: aaaJava HBase client - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Maven toobuild een op Java gebaseerde Apache HBase-toepassing, implementeert u deze tooHBase in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="6580e-103">Java-toepassingen voor Apache HBase bouwen</span><span class="sxs-lookup"><span data-stu-id="6580e-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="6580e-104">Meer informatie over hoe toocreate een [Apache HBase](http://hbase.apache.org/) toepassing in Java.</span><span class="sxs-lookup"><span data-stu-id="6580e-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="6580e-105">Vervolgens Hallo toepassing gebruiken met HBase op Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6580e-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="6580e-106">Hallo stappen in dit document [Maven](http://maven.apache.org/) toocreate en build Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="6580e-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="6580e-107">Maven is een beheer van software-project en begrip hulpprogramma waarmee u toobuild software, documentatie en rapporten voor Java-projecten.</span><span class="sxs-lookup"><span data-stu-id="6580e-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="6580e-108">Hallo zijn stappen in dit document meest recent getest met HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="6580e-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6580e-109">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="6580e-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6580e-110">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6580e-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6580e-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6580e-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="6580e-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6580e-112">Requirements</span></span>

* <span data-ttu-id="6580e-113">[Java-platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6580e-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6580e-114">HDInsight 3.5 en groter vereist Java 8.</span><span class="sxs-lookup"><span data-stu-id="6580e-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="6580e-115">Eerdere versies van HDInsight vereisen Java 7.</span><span class="sxs-lookup"><span data-stu-id="6580e-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="6580e-116">Maven</span><span class="sxs-lookup"><span data-stu-id="6580e-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="6580e-117">Een Azure HDInsight op basis van Linux-cluster met HBase</span><span class="sxs-lookup"><span data-stu-id="6580e-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="6580e-118">Hallo stappen in dit document is getest met HDInsight-cluster versie 3.4 en 3.5.</span><span class="sxs-lookup"><span data-stu-id="6580e-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="6580e-119">Hallo-standaardwaarden die is opgegeven in de voorbeelden zijn voor een 3.5 HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="6580e-120">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="6580e-120">Create hello project</span></span>

1. <span data-ttu-id="6580e-121">Wijzig vanaf de opdrachtregel Hallo in uw ontwikkelomgeving, mappen toohello locatie waar u toocreate Hallo-project, bijvoorbeeld `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="6580e-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="6580e-122">Gebruik Hallo **mvn** opdracht, die is geïnstalleerd met Maven, toogenerate hello scaffolding voor Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="6580e-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="6580e-123">Als u met behulp van PowerShell, moet u Hallo tussen `-D` parameters tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="6580e-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="6580e-124">Met deze opdracht maakt u een map met dezelfde naam als Hallo Hallo **artefact-id** parameter (**hbaseapp** in dit voorbeeld.) Deze map bevat de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="6580e-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="6580e-125">**pom.XML**: Hallo Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) gegevens en configuratie details gebruikt toobuild Hallo-project bevat.</span><span class="sxs-lookup"><span data-stu-id="6580e-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="6580e-126">**SRC**: Hallo-map met de Hallo **main/java/com/microsoft/voorbeelden** directory, waar u de toepassing hello schrijven.</span><span class="sxs-lookup"><span data-stu-id="6580e-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="6580e-127">Hallo verwijderen `src/test/java/com/microsoft/examples/apptest.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="6580e-128">Het is niet in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6580e-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="6580e-129">Hallo Project Object Model bijwerken</span><span class="sxs-lookup"><span data-stu-id="6580e-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="6580e-130">Hallo bewerken `pom.xml` bestands- en toevoegen van de volgende code in Hallo Hallo `<dependencies>` sectie:</span><span class="sxs-lookup"><span data-stu-id="6580e-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="6580e-131">Deze sectie geeft aan dat project Hallo moet **hbase-client** en **phoenix-core** onderdelen.</span><span class="sxs-lookup"><span data-stu-id="6580e-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="6580e-132">Tijdens het compileren worden van Hallo standaard Maven opslagplaats deze afhankelijkheden gedownload.</span><span class="sxs-lookup"><span data-stu-id="6580e-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="6580e-133">U kunt Hallo [Maven centrale opslagplaats zoeken](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn meer informatie over deze afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="6580e-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="6580e-134">Hallo-versienummer van Hallo hbase-client moet overeenkomen met de Hallo-versie van HBase die beschikbaar is in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="6580e-135">Gebruik Hallo volgende tabel toofind Hallo juiste versienummer.</span><span class="sxs-lookup"><span data-stu-id="6580e-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="6580e-136">HDInsight-cluster versie</span><span class="sxs-lookup"><span data-stu-id="6580e-136">HDInsight cluster version</span></span> | <span data-ttu-id="6580e-137">HBase versie toouse</span><span class="sxs-lookup"><span data-stu-id="6580e-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="6580e-138">3.2</span><span class="sxs-lookup"><span data-stu-id="6580e-138">3.2</span></span> |<span data-ttu-id="6580e-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="6580e-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="6580e-140">3.3, 3.4 3.5 en 3.6</span><span class="sxs-lookup"><span data-stu-id="6580e-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="6580e-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="6580e-141">1.1.2</span></span> |

    <span data-ttu-id="6580e-142">Zie voor meer informatie over de versies van HDInsight en -onderdelen [wat Hallo andere Hadoop-onderdelen beschikbaar met HDInsight zijn](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6580e-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="6580e-143">Hallo na code toohello toevoegen **pom.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="6580e-144">Deze tekst moet binnen Hallo `<project>...</project>` labels in Hallo-bestand, bijvoorbeeld tussen `</dependencies>` en `</project>`.</span><span class="sxs-lookup"><span data-stu-id="6580e-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
            </configuration>
            <executions>
            <execution>
                <phase>package</phase>
                <goals>
                <goal>shade</goal>
                </goals>
            </execution>
            </executions>
        </plugin>
        </plugins>
    </build>
   ```

    <span data-ttu-id="6580e-145">Deze sectie configureert u een resource (`conf/hbase-site.xml`) die configuratie-informatie voor HBase bevat.</span><span class="sxs-lookup"><span data-stu-id="6580e-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6580e-146">U kunt ook configuratiewaarden via code instellen.</span><span class="sxs-lookup"><span data-stu-id="6580e-146">You can also set configuration values via code.</span></span> <span data-ttu-id="6580e-147">Zie Hallo opmerkingen in Hallo `CreateTable` voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6580e-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="6580e-148">Deze sectie configureert ook Hallo [Maven-Compiler-invoegtoepassing](http://maven.apache.org/plugins/maven-compiler-plugin/) en [Maven grijs-invoegtoepassing](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="6580e-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="6580e-149">Hallo-compiler invoegtoepassing is gebruikte toocompile Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="6580e-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="6580e-150">Hallo tint invoegtoepassing is gebruikte tooprevent licentie duplicatie in Hallo JAR-pakket dat wordt gebouwd door Maven.</span><span class="sxs-lookup"><span data-stu-id="6580e-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="6580e-151">Deze invoegtoepassing gebruikte tooprevent is een fout, 'dubbele licentiebestanden' tijdens runtime op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="6580e-152">Met behulp van maven-schaduw-invoegtoepassing Hello `ApacheLicenseResourceTransformer` implementatie Hallo fout voorkomt.</span><span class="sxs-lookup"><span data-stu-id="6580e-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="6580e-153">Hallo maven-schaduw-invoegtoepassing produceert ook een uber jar dat alle vereiste door Hallo toepassing hello afhankelijkheden bevat.</span><span class="sxs-lookup"><span data-stu-id="6580e-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="6580e-154">Hallo opslaan `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="6580e-155">Maak een map met de naam `conf` in Hallo `hbaseapp` directory.</span><span class="sxs-lookup"><span data-stu-id="6580e-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="6580e-156">Deze map is gebruikte toohold configuratie-informatie voor het verbinden van tooHBase.</span><span class="sxs-lookup"><span data-stu-id="6580e-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="6580e-157">Gebruik Hallo volgende opdracht toocopy hello HBase configuratie uit Hallo HBase-cluster toohello `conf` directory.</span><span class="sxs-lookup"><span data-stu-id="6580e-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="6580e-158">Vervang `USERNAME` met Hallo-naam van uw SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6580e-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="6580e-159">Vervang `CLUSTERNAME` met de naam van uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="6580e-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="6580e-160">Voor meer informatie over het gebruik van `ssh` en `scp`, Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6580e-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="6580e-161">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="6580e-161">Create hello application</span></span>

1. <span data-ttu-id="6580e-162">Ga toohello `hbaseapp/src/main/java/com/microsoft/examples` map en wijzig de naam Hallo u bestand app.java te`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="6580e-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="6580e-163">Open Hallo `CreateTable.java` bestand en vervang de bestaande inhoud Hallo door Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="6580e-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="6580e-164">Deze code is Hallo **CreateTable** klasse, die u een tabel met de naam maakt **mensen** en deze vullen met een aantal vooraf gedefinieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6580e-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="6580e-165">Hallo opslaan `CreateTable.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="6580e-166">In Hallo `hbaseapp/src/main/java/com/microsoft/examples` directory, maakt u een bestand met de naam `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="6580e-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="6580e-167">Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="6580e-167">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="6580e-168">Hallo **SearchByEmail** klasse kan worden gebruikt tooquery voor rijen door e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="6580e-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="6580e-169">Omdat een filter reguliere expressie worden gebruikt, kunt u een tekenreeks of een reguliere expressie opgeven wanneer u Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="6580e-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="6580e-170">Hallo opslaan `SearchByEmail.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="6580e-171">In Hallo `hbaseapp/src/main/hava/com/microsoft/examples` directory, maakt u een bestand met de naam `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="6580e-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="6580e-172">Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="6580e-172">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="6580e-173">Deze klasse is ruimt Hallo waarvan in dit voorbeeld is gemaakt door het uitschakelen van HBase-tabellen en neer te zetten Hallo tabel gemaakt door Hallo `CreateTable` klasse.</span><span class="sxs-lookup"><span data-stu-id="6580e-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="6580e-174">Hallo opslaan `DeleteTable.java` bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="6580e-175">Hallo-toepassing bouwen en pakket</span><span class="sxs-lookup"><span data-stu-id="6580e-175">Build and package hello application</span></span>

1. <span data-ttu-id="6580e-176">Van Hallo `hbaseapp` map gebruik Hallo volgende opdracht toobuild een JAR-bestand dat de toepassing hello bevat:</span><span class="sxs-lookup"><span data-stu-id="6580e-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="6580e-177">Met deze opdracht maakt en pakketten Hallo toepassing naar een JAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="6580e-178">Wanneer Hallo-opdracht is voltooid, hello `hbaseapp/target` map bevat een bestand met de naam `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="6580e-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6580e-179">Hallo `hbaseapp-1.0-SNAPSHOT.jar` bestand is een jar uber.</span><span class="sxs-lookup"><span data-stu-id="6580e-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="6580e-180">Deze bevat alle Hallo afhankelijkheden vereist toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6580e-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="6580e-181">Hallo JAR uploaden en uitvoeren van taken (SSH)</span><span class="sxs-lookup"><span data-stu-id="6580e-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="6580e-182">Hallo na gebruik van de stappen `scp` toocopy Hallo JAR toohello primaire hoofdknooppunt van uw HBase op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="6580e-183">Hallo `ssh` opdracht tooconnect toohello cluster gebruikt en het Hallo-voorbeeld uitvoeren rechtstreeks op het hoofdknooppunt Hallo is.</span><span class="sxs-lookup"><span data-stu-id="6580e-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="6580e-184">tooupload hello jar toohello cluster, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="6580e-185">Vervang `USERNAME` met Hallo-naam van uw SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6580e-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="6580e-186">Vervang `CLUSTERNAME` met de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="6580e-187">tooconnect toohello HBase-cluster gebruiken Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="6580e-188">Vervang `USERNAME` Hallo-naam van uw SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6580e-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="6580e-189">Vervang `CLUSTERNAME` met de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="6580e-190">een HBase-tabel met toocreate Hallo Java-toepassing, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="6580e-191">Deze opdracht maakt u een HBase-tabel met de naam **mensen**, en gevuld met gegevens.</span><span class="sxs-lookup"><span data-stu-id="6580e-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="6580e-192">toosearch voor e-mailadressen die zijn opgeslagen in tabel hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="6580e-193">U ontvangt Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="6580e-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="6580e-194">toodelete hello tabel Gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="6580e-195">Uploaden van Hallo JAR-taken en uitvoeren (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6580e-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="6580e-196">Hallo stappen te volgen gebruik Azure PowerShell tooupload Hallo JAR toohello standaard opslag voor uw HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="6580e-197">HDInsight-cmdlets worden vervolgens gebruikt toorun Hallo voorbeelden op afstand.</span><span class="sxs-lookup"><span data-stu-id="6580e-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="6580e-198">Nadat het installeren en configureren van Azure PowerShell, maakt u een bestand met de naam `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="6580e-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="6580e-199">Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="6580e-199">Use hello following text as hello contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="6580e-200">Dit bestand bevat twee modules:</span><span class="sxs-lookup"><span data-stu-id="6580e-200">This file contains two modules:</span></span>

   * <span data-ttu-id="6580e-201">**Voeg HDInsightFile** : wordt gebruikt tooupload bestanden toohello cluster</span><span class="sxs-lookup"><span data-stu-id="6580e-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="6580e-202">**Start HBaseExample** -toorun Hallo klassen eerder hebt gemaakt die wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="6580e-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="6580e-203">Hallo opslaan `hbase-runner.psm1` bestand.</span><span class="sxs-lookup"><span data-stu-id="6580e-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="6580e-204">Een nieuw Azure PowerShell-venster openen, wijzigen van mappen toohello `hbaseapp` directory, en vervolgens uitvoeren Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="6580e-205">Wijzig Hallo pad toohello locatie Hallo `hbase-runner.psm1` bestand eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6580e-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="6580e-206">Deze opdracht wordt de module Hallo geregistreerd met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6580e-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="6580e-207">Gebruik Hallo volgende opdracht tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="6580e-208">Vervang `hdinsightclustername` met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="6580e-209">Hallo opdracht uploadt Hallo `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` locatie in Hallo primaire opslag voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="6580e-210">een tabel met toocreate Hallo `hbaseapp`, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6580e-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="6580e-211">Vervang `hdinsightclustername` met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="6580e-212">Met deze opdracht maakt een tabel met de naam **mensen** in HBase op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="6580e-213">Met deze opdracht wordt geen uitvoer niet weergegeven in het consolevenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="6580e-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="6580e-214">toosearch voor vermeldingen in de tabel hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6580e-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="6580e-215">Vervang `hdinsightclustername` met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6580e-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="6580e-216">Met deze opdracht maakt gebruik van Hallo `SearchByEmail` klasse toosearch voor rijen waar hello `contactinformation` kolomfamilie en Hallo `email` kolom Hallo tekenreeks bevat `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="6580e-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="6580e-217">U ontvangt Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="6580e-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="6580e-218">Met behulp van **fabrikam.com** voor Hallo `-emailRegex` waarde retourneert Hallo-gebruikers die hebben **fabrikam.com** in Hallo e-veld.</span><span class="sxs-lookup"><span data-stu-id="6580e-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="6580e-219">U kunt ook reguliere expressies gebruiken als Hallo zoekterm.</span><span class="sxs-lookup"><span data-stu-id="6580e-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="6580e-220">Bijvoorbeeld: **^ r** retourneert e-mailadressen die met een letter Hallo 'r beginnen'.</span><span class="sxs-lookup"><span data-stu-id="6580e-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="6580e-221">Er zijn geen resultaten of onverwachte resultaten optreden wanneer u Start HBaseExample</span><span class="sxs-lookup"><span data-stu-id="6580e-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="6580e-222">Gebruik Hallo `-showErr` parameter tooview Hallo standaardfout (STDERR) dat wordt gegenereerd tijdens het Hallo-taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6580e-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="6580e-223">Hallo-tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="6580e-223">Delete hello table</span></span>

<span data-ttu-id="6580e-224">Wanneer u klaar bent met het Hallo-voorbeeld gebruiken na toodelete Hallo Hallo **mensen** tabel die wordt gebruikt in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6580e-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="6580e-225">__Van een `ssh` sessie__:</span><span class="sxs-lookup"><span data-stu-id="6580e-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="6580e-226">__Vanuit Azure PowerShell__:</span><span class="sxs-lookup"><span data-stu-id="6580e-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="6580e-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6580e-227">Next steps</span></span>

[<span data-ttu-id="6580e-228">Meer informatie over hoe toouse SQuirreL SQL met HBase</span><span class="sxs-lookup"><span data-stu-id="6580e-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
