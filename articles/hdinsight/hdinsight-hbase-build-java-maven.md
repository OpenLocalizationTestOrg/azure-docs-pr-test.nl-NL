---
title: een Java-HBase-toepassing voor op basis van Windows Azure HDInsight aaaBuild | Microsoft Docs
description: Meer informatie over hoe toouse Apache Maven toobuild een op Java gebaseerde Apache HBase-toepassing, implementeert u deze tooa op basis van Windows Azure HDInsight-cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="99c64-103">Maven toobuild Java-toepassingen die gebruikmaken van HBase met HDInsight (Hadoop) op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="99c64-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="99c64-104">Meer informatie over hoe toocreate en bouwen van een [Apache HBase](http://hbase.apache.org/) toepassing in Java met behulp van Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="99c64-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="99c64-105">Vervolgens Hallo toepassing gebruiken met Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="99c64-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="99c64-106">[Maven](http://maven.apache.org/) is een software-project management en begrip hulpprogramma waarmee u toobuild software, documentatie en rapporten voor Java-projecten.</span><span class="sxs-lookup"><span data-stu-id="99c64-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="99c64-107">In dit artikel leert u hoe toouse het toocreate een basic Java-toepassing die wordt gemaakt, zoekt en verwijdert een HBase tabel in een Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99c64-108">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Windows.</span><span class="sxs-lookup"><span data-stu-id="99c64-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="99c64-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="99c64-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="99c64-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="99c64-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="99c64-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="99c64-111">Requirements</span></span>
* <span data-ttu-id="99c64-112">[Java-platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="99c64-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="99c64-113">Maven</span><span class="sxs-lookup"><span data-stu-id="99c64-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="99c64-114">Een cluster met HBase met HDInsight op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="99c64-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="99c64-115">Hallo stappen in dit document is getest met HDInsight-cluster versie 3.2 en 3.3.</span><span class="sxs-lookup"><span data-stu-id="99c64-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="99c64-116">Hallo-standaardwaarden die is opgegeven in de voorbeelden zijn voor een 3.3 HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="99c64-117">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="99c64-117">Create hello project</span></span>
1. <span data-ttu-id="99c64-118">Wijzig vanaf de opdrachtregel Hallo in uw ontwikkelomgeving, mappen toohello locatie waar u toocreate Hallo-project, bijvoorbeeld `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="99c64-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="99c64-119">Gebruik Hallo **mvn** opdracht, die is geïnstalleerd met Maven, toogenerate hello scaffolding voor Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="99c64-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="99c64-120">Deze opdracht maakt een map in de huidige locatie Hallo met Hallo door Hallo opgegeven **artefact-id** parameter (**hbaseapp** in dit voorbeeld.) Deze map bevat de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="99c64-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="99c64-121">**pom.XML**: Hallo Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) gegevens en configuratie details gebruikt toobuild Hallo-project bevat.</span><span class="sxs-lookup"><span data-stu-id="99c64-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="99c64-122">**SRC**: Hallo-map met de Hallo **main\java\com\microsoft\examples** directory, waar u de toepassing hello wordt schrijven.</span><span class="sxs-lookup"><span data-stu-id="99c64-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="99c64-123">Hallo verwijderen **src\test\java\com\microsoft\examples\apptest.java** bestand omdat deze niet wordt gebruikt in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="99c64-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="99c64-124">Hallo Project Object Model bijwerken</span><span class="sxs-lookup"><span data-stu-id="99c64-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="99c64-125">Hallo bewerken **pom.xml** bestands- en toevoegen van de volgende code in Hallo Hallo `<dependencies>` sectie:</span><span class="sxs-lookup"><span data-stu-id="99c64-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="99c64-126">Dit gedeelte wordt uitgelegd Maven die Hallo project vereist **hbase-client** versie **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="99c64-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="99c64-127">Tijdens de compilatie, wordt deze afhankelijkheid gedownload van Hallo standaard Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="99c64-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="99c64-128">U kunt Hallo [Maven centrale opslagplaats zoeken](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn meer informatie over deze afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="99c64-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="99c64-129">Hallo-versienummer moet overeenkomen met de Hallo-versie van HBase die beschikbaar is in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="99c64-130">Gebruik Hallo volgende tabel toofind Hallo juiste versienummer.</span><span class="sxs-lookup"><span data-stu-id="99c64-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="99c64-131">HDInsight-cluster versie</span><span class="sxs-lookup"><span data-stu-id="99c64-131">HDInsight cluster version</span></span> | <span data-ttu-id="99c64-132">HBase versie toouse</span><span class="sxs-lookup"><span data-stu-id="99c64-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="99c64-133">3.2</span><span class="sxs-lookup"><span data-stu-id="99c64-133">3.2</span></span> |<span data-ttu-id="99c64-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="99c64-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="99c64-135">3.3</span><span class="sxs-lookup"><span data-stu-id="99c64-135">3.3</span></span> |<span data-ttu-id="99c64-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="99c64-136">1.1.2</span></span> |

    <span data-ttu-id="99c64-137">Zie voor meer informatie over de versies van HDInsight en -onderdelen [wat Hallo andere Hadoop-onderdelen beschikbaar met HDInsight zijn](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="99c64-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="99c64-138">Als u een 3.3 HDInsight-cluster gebruikt, moet u ook na toohello Hallo toevoegen `<dependencies>` sectie:</span><span class="sxs-lookup"><span data-stu-id="99c64-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="99c64-139">Deze afhankelijkheid laadt Hallo phoenix core-onderdelen, die worden gebruikt door Hbase versie 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="99c64-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="99c64-140">Hallo na code toohello toevoegen **pom.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="99c64-141">Deze sectie moet binnen Hallo `<project>...</project>` labels in Hallo-bestand, bijvoorbeeld tussen `</dependencies>` en `</project>`.</span><span class="sxs-lookup"><span data-stu-id="99c64-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="99c64-142">Hallo `<resources>` sectie configureert u een resource (**conf\hbase site.xml**) die configuratie-informatie voor HBase bevat.</span><span class="sxs-lookup"><span data-stu-id="99c64-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99c64-143">U kunt ook configuratiewaarden via code instellen.</span><span class="sxs-lookup"><span data-stu-id="99c64-143">You can also set configuration values via code.</span></span> <span data-ttu-id="99c64-144">Zie Hallo opmerkingen in Hallo **CreateTable** voor het volgende voorbeeld toodo dit.</span><span class="sxs-lookup"><span data-stu-id="99c64-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="99c64-145">Dit `<plugins>` sectie configureert u Hallo [Maven-Compiler-invoegtoepassing](http://maven.apache.org/plugins/maven-compiler-plugin/) en [Maven grijs-invoegtoepassing](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="99c64-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="99c64-146">Hallo-compiler invoegtoepassing is gebruikte toocompile Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="99c64-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="99c64-147">Hallo tint invoegtoepassing is gebruikte tooprevent licentie duplicatie in Hallo JAR-pakket dat wordt gebouwd door Maven.</span><span class="sxs-lookup"><span data-stu-id="99c64-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="99c64-148">Hallo reden die wordt gebruikt, is Hallo dubbele licentiebestanden veroorzaakt een fout tijdens de uitvoering op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="99c64-149">Met behulp van maven-schaduw-invoegtoepassing Hello `ApacheLicenseResourceTransformer` implementatie wordt voorkomen dat deze fout.</span><span class="sxs-lookup"><span data-stu-id="99c64-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="99c64-150">Hallo schaduw-maven-invoegtoepassing ook produceert een uber jar (of jar fat) dat alle vereiste door Hallo toepassing hello afhankelijkheden bevat.</span><span class="sxs-lookup"><span data-stu-id="99c64-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="99c64-151">Hallo opslaan **pom.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="99c64-152">Maak een nieuwe map met de naam **conf** in Hallo **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="99c64-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="99c64-153">In Hallo **conf** directory, maakt u een bestand met de naam **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="99c64-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="99c64-154">Volgende Hallo als Hallo inhoud van Hallo-bestand gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99c64-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="99c64-155">Dit bestand worden gebruikte tooload hello HBase-configuratie voor een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99c64-156">Dit is een minimale hbase-site.xml-bestand en Hallo bare minimale instellingen voor Hallo HDInsight-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="99c64-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="99c64-157">Hallo opslaan **hbase-site.xml** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="99c64-158">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="99c64-158">Create hello application</span></span>
1. <span data-ttu-id="99c64-159">Ga toohello **hbaseapp\src\main\java\com\microsoft\examples** map en wijzig de naam Hallo u bestand app.java te**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="99c64-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="99c64-160">Open Hallo **CreateTable.java** bestand en vervang de bestaande inhoud Hallo door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="99c64-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="99c64-161">Dit is Hallo **CreateTable** klasse, die een tabel met de naam **mensen** en deze vullen met een aantal vooraf gedefinieerde gebruikers.</span><span class="sxs-lookup"><span data-stu-id="99c64-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="99c64-162">Hallo opslaan **CreateTable.java** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="99c64-163">In Hallo **hbaseapp\src\main\java\com\microsoft\examples** directory, maak een nieuw bestand met de naam **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="99c64-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="99c64-164">Gebruik Hallo code als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="99c64-164">Use hello following code as hello contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="99c64-165">Hallo **SearchByEmail** klasse kan worden gebruikt tooquery voor rijen door e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="99c64-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="99c64-166">Omdat een filter reguliere expressie worden gebruikt, kunt u een tekenreeks of een reguliere expressie opgeven wanneer u Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="99c64-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="99c64-167">Hallo opslaan **SearchByEmail.java** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="99c64-168">In Hallo **hbaseapp\src\main\hava\com\microsoft\examples** directory, maak een nieuw bestand met de naam **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="99c64-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="99c64-169">Gebruik Hallo code als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="99c64-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="99c64-170">Deze klasse is voor het opruimen van dit voorbeeld door uit te schakelen en neer te zetten Hallo tabel gemaakt door Hallo **CreateTable** klasse.</span><span class="sxs-lookup"><span data-stu-id="99c64-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="99c64-171">Hallo opslaan **DeleteTable.java** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="99c64-172">Hallo-toepassing bouwen en pakket</span><span class="sxs-lookup"><span data-stu-id="99c64-172">Build and package hello application</span></span>
1. <span data-ttu-id="99c64-173">Open een opdrachtprompt en wijzig de mappen toohello **hbaseapp** directory.</span><span class="sxs-lookup"><span data-stu-id="99c64-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="99c64-174">Hallo opdracht toobuild een JAR-bestand dat de toepassing hello bevat volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99c64-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="99c64-175">Dit schoongemaakt eventuele vorige build-artefacten, downloadt eventuele afhankelijkheden die nog niet hebt geïnstalleerd, klikt u vervolgens bouwt en toepassing hello-pakketten.</span><span class="sxs-lookup"><span data-stu-id="99c64-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="99c64-176">Wanneer Hallo-opdracht is voltooid, hello **hbaseapp\target** map bevat een bestand met de naam **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="99c64-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99c64-177">Hallo **hbaseapp-1.0-SNAPSHOT.jar** bestand is een uber jar (ook wel een fat jar genoemd) waarin alle Hallo afhankelijkheden toorun Hallo toepassing vereist.</span><span class="sxs-lookup"><span data-stu-id="99c64-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="99c64-178">Hallo JAR-bestand uploaden en start een taak</span><span class="sxs-lookup"><span data-stu-id="99c64-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="99c64-179">Er zijn veel manieren tooupload een bestand tooyour HDInsight-cluster, zoals beschreven in [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="99c64-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="99c64-180">Hallo volgende stappen gebruikt Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99c64-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="99c64-181">Nadat het installeren en configureren van Azure PowerShell, maakt een nieuw bestand met de naam **hbase runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="99c64-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="99c64-182">De volgende Hallo als Hallo inhoud van dit bestand gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99c64-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="99c64-183">Dit bestand bevat twee modules:</span><span class="sxs-lookup"><span data-stu-id="99c64-183">This file contains two modules:</span></span>

   * <span data-ttu-id="99c64-184">**Voeg HDInsightFile** -tooupload bestanden tooHDInsight gebruikt</span><span class="sxs-lookup"><span data-stu-id="99c64-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="99c64-185">**Start HBaseExample** -toorun Hallo klassen eerder hebt gemaakt die wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="99c64-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="99c64-186">Hallo opslaan **hbase runner.psm1** bestand.</span><span class="sxs-lookup"><span data-stu-id="99c64-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="99c64-187">Een nieuw Azure PowerShell-venster openen, wijzigen van mappen toohello **hbaseapp** directory, en vervolgens uitvoeren Hallo opdracht.</span><span class="sxs-lookup"><span data-stu-id="99c64-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="99c64-188">Wijzig Hallo pad toohello locatie Hallo **hbase runner.psm1** bestand eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="99c64-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="99c64-189">Dit Hallo module hebt geregistreerd voor deze Azure PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="99c64-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="99c64-190">Gebruik Hallo volgende opdracht tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="99c64-191">Vervang **hdinsightclustername** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="99c64-192">Hallo opdracht uploadt Hallo **hbaseapp-1.0-SNAPSHOT.jar** toohello **voorbeeld/potten** locatie in Hallo primaire opslag voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="99c64-193">Nadat het Hallo-bestanden zijn geüpload, gebruik Hallo volgende code toocreate een tabel met behulp van Hallo **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="99c64-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="99c64-194">Vervang **hdinsightclustername** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="99c64-195">Deze opdracht maakt u een nieuwe tabel met de naam **mensen** in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="99c64-196">Met deze opdracht wordt geen uitvoer niet weergegeven in het consolevenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="99c64-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="99c64-197">toosearch voor vermeldingen in de tabel hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="99c64-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="99c64-198">Vervang **hdinsightclustername** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="99c64-199">Met deze opdracht maakt gebruik van Hallo **SearchByEmail** klasse toosearch voor rijen waar hello **contactinformation** kolomfamilie en Hallo **e** kolom Hallo tekenreeks bevat **contoso.com**. U ontvangt Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="99c64-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="99c64-200">Met behulp van **fabrikam.com** voor Hallo `-emailRegex` waarde retourneert Hallo-gebruikers die hebben **fabrikam.com** in Hallo e-veld.</span><span class="sxs-lookup"><span data-stu-id="99c64-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="99c64-201">Aangezien deze zoekopdracht wordt geïmplementeerd met behulp van een reguliere expressie gebaseerde filter, u kunt ook opgeven reguliere expressies, zoals **^ r**, welke retourneert posten waarbij Hallo e-mailadres met de Hallo letter 'r begint'.</span><span class="sxs-lookup"><span data-stu-id="99c64-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="99c64-202">Hallo-tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="99c64-202">Delete hello table</span></span>
<span data-ttu-id="99c64-203">Wanneer u klaar bent met het Hallo-voorbeeld, gebruik Hallo volgende opdracht uit hello Azure PowerShell-sessie toodelete hello **mensen** tabel die wordt gebruikt in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="99c64-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="99c64-204">Vervang **hdinsightclustername** met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="99c64-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="99c64-205">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="99c64-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="99c64-206">Er zijn geen resultaten of onverwachte resultaten optreden wanneer u Start HBaseExample</span><span class="sxs-lookup"><span data-stu-id="99c64-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="99c64-207">Gebruik Hallo `-showErr` parameter tooview Hallo standaardfout (STDERR) dat wordt gegenereerd tijdens het Hallo-taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99c64-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
