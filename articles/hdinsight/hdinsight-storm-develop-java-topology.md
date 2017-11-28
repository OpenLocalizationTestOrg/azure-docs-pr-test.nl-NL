---
title: aaaApache Storm-voorbeeld Java-topologie - Azure HDInsight | Microsoft Docs
description: "Meer informatie over hoe toocreate Apache Storm-topologieën in Java door het maken van een voorbeeldwoord topologie tellen."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: Apache storm, apache storm bijvoorbeeld storm java, storm-topologie-voorbeeld
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="9017a-104">Maken van een Apache Storm-topologie in Java</span><span class="sxs-lookup"><span data-stu-id="9017a-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="9017a-105">Meer informatie over hoe toocreate een op Java gebaseerde topologie voor Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="9017a-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="9017a-106">U maakt een Storm-topologie die een word-count-toepassing implementeert.</span><span class="sxs-lookup"><span data-stu-id="9017a-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="9017a-107">U Maven toobuild en pakket Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="9017a-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="9017a-108">Vervolgens leert u hoe toodefine Hallo topologie gebruik Hallo lichtstroom framework.</span><span class="sxs-lookup"><span data-stu-id="9017a-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="9017a-109">Hallo lichtstroom framework is beschikbaar in Storm 0.10.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9017a-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="9017a-110">Storm 0.10.0 is beschikbaar met HDInsight 3.3 en 3.4.</span><span class="sxs-lookup"><span data-stu-id="9017a-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="9017a-111">U kunt na het voltooien van de stappen in dit document Hallo Hallo topologie tooApache Storm op HDInsight implementeren.</span><span class="sxs-lookup"><span data-stu-id="9017a-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="9017a-112">Er is een voltooide versie van Hallo Storm-topologie voorbeelden gemaakt in dit document beschikbaar op [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="9017a-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9017a-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9017a-113">Prerequisites</span></span>

* [<span data-ttu-id="9017a-114">Java Developer Kit (JDK) versie 7</span><span class="sxs-lookup"><span data-stu-id="9017a-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="9017a-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is een project build-systeem voor Java-projecten.</span><span class="sxs-lookup"><span data-stu-id="9017a-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="9017a-116">Een teksteditor of IDE.</span><span class="sxs-lookup"><span data-stu-id="9017a-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="9017a-117">Omgevingsvariabelen configureren</span><span class="sxs-lookup"><span data-stu-id="9017a-117">Configure environment variables</span></span>

<span data-ttu-id="9017a-118">Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK installeert.</span><span class="sxs-lookup"><span data-stu-id="9017a-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="9017a-119">Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="9017a-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="9017a-120">**JAVA_HOME** -toohello directory waar Hallo Java runtime environment (JRE) is geïnstalleerd moet verwijzen.</span><span class="sxs-lookup"><span data-stu-id="9017a-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="9017a-121">Bijvoorbeeld in een Unix- of Linux-distributie, heeft een waarde gelijkaardig te`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="9017a-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="9017a-122">In Windows, zou er een waarde gelijkaardig te`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="9017a-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="9017a-123">**PAD** -moet bevatten Hallo paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="9017a-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="9017a-124">**JAVA_HOME** (of equivalente paden Hallo)</span><span class="sxs-lookup"><span data-stu-id="9017a-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="9017a-125">**JAVA_HOME\bin** (of equivalente paden Hallo)</span><span class="sxs-lookup"><span data-stu-id="9017a-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="9017a-126">Hallo-directory waar Maven is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="9017a-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="9017a-127">Een Maven-project maken</span><span class="sxs-lookup"><span data-stu-id="9017a-127">Create a Maven project</span></span>

<span data-ttu-id="9017a-128">Vanaf de opdrachtregel Hallo gebruik Hallo volgende opdracht toocreate een Maven-project met de naam **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="9017a-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="9017a-129">Als u met behulp van PowerShell, moet u tussen de`-D` parameters met dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="9017a-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="9017a-130">Deze opdracht maakt u een map met de naam `WordCount` op Hallo huidige locatie, die een basic Maven-project bevat.</span><span class="sxs-lookup"><span data-stu-id="9017a-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="9017a-131">Hallo `WordCount` map bevat Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="9017a-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="9017a-132">`pom.xml`: Bevat instellingen voor Hallo Maven-project.</span><span class="sxs-lookup"><span data-stu-id="9017a-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="9017a-133">`src\main\java\com\microsoft\example`: Bevat de toepassingscode van uw.</span><span class="sxs-lookup"><span data-stu-id="9017a-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="9017a-134">`src\test\java\com\microsoft\example`: Bevat de tests voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9017a-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="9017a-135">Voorbeeldcode Hallo gegenereerd verwijderen</span><span class="sxs-lookup"><span data-stu-id="9017a-135">Remove hello generated example code</span></span>

<span data-ttu-id="9017a-136">Hallo gegenereerd test en toepassingsbestanden Hallo verwijderen:</span><span class="sxs-lookup"><span data-stu-id="9017a-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="9017a-137">**src\test\java\com\microsoft\example\AppTest.Java**</span><span class="sxs-lookup"><span data-stu-id="9017a-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="9017a-138">**src\main\java\com\microsoft\example\App.Java**</span><span class="sxs-lookup"><span data-stu-id="9017a-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="9017a-139">Maven-opslagplaatsen toevoegen</span><span class="sxs-lookup"><span data-stu-id="9017a-139">Add Maven repositories</span></span>

<span data-ttu-id="9017a-140">HDInsight is gebaseerd op Hallo Hortonworks Data Platform HDP (), zodat u wordt aangeraden Hallo Hortonworks opslagplaats toodownload afhankelijkheden voor uw Apache Storm-projecten.</span><span class="sxs-lookup"><span data-stu-id="9017a-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="9017a-141">In Hallo __pom.xml__ bestand, het toevoegen van XML te volgen nadat Hallo Hallo `<url>http://maven.apache.org</url>` regel:</span><span class="sxs-lookup"><span data-stu-id="9017a-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="9017a-142">Eigenschappen toevoegen</span><span class="sxs-lookup"><span data-stu-id="9017a-142">Add properties</span></span>

<span data-ttu-id="9017a-143">Maven kunt u toodefine projectniveau waarden ' Eigenschappen ' genoemd.</span><span class="sxs-lookup"><span data-stu-id="9017a-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="9017a-144">In Hallo __pom.xml__, toevoegen na tekst na Hallo Hallo `</repositories>` regel:</span><span class="sxs-lookup"><span data-stu-id="9017a-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="9017a-145">U kunt deze waarde nu gebruiken in andere gedeelten van Hallo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="9017a-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="9017a-146">Bijvoorbeeld, wanneer u opgeeft Hallo-versie van Storm-onderdelen, kunt u `${storm.version}` in plaats van een vaste waarde coderen.</span><span class="sxs-lookup"><span data-stu-id="9017a-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="9017a-147">Afhankelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="9017a-147">Add dependencies</span></span>

<span data-ttu-id="9017a-148">Een afhankelijkheid voor Storm-onderdelen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9017a-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="9017a-149">Open Hallo `pom.xml` bestands- en toevoegen van de volgende code in Hallo Hallo `<dependencies>` sectie:</span><span class="sxs-lookup"><span data-stu-id="9017a-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="9017a-150">Tijdens het compileren Maven maakt gebruik van deze informatie toolook up `storm-core` in Hallo Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9017a-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="9017a-151">Eerst wordt gezocht in de opslagplaats Hallo op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="9017a-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="9017a-152">Als er niet zijn Hallo-bestanden, wordt Maven downloadt deze vanuit openbare opslagplaats met Maven Hallo en opgeslagen in de lokale Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="9017a-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="9017a-153">Kennisgeving Hallo `<scope>provided</scope>` regel in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="9017a-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="9017a-154">Deze instelling geeft Maven tooexclude **storm-core** van JAR-bestanden die zijn gemaakt, omdat dit wordt geleverd door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="9017a-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="9017a-155">Configuratie maken</span><span class="sxs-lookup"><span data-stu-id="9017a-155">Build configuration</span></span>

<span data-ttu-id="9017a-156">Maven-invoegtoepassingen toestaan toocustomize Hallo build fasen van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="9017a-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="9017a-157">Bijvoorbeeld, hoe Hallo project is gecompileerd of hoe toopackage in een JAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="9017a-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="9017a-158">Open Hallo `pom.xml` bestands- en toevoegen van de volgende code direct boven Hallo Hallo `</project>` regel.</span><span class="sxs-lookup"><span data-stu-id="9017a-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="9017a-159">Deze sectie is gebruikte tooadd invoegtoepassingen, bronnen en andere configuratieopties build.</span><span class="sxs-lookup"><span data-stu-id="9017a-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="9017a-160">Voor een volledige beschrijving van Hallo **pom.xml** bestand, Zie [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="9017a-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="9017a-161">Invoegtoepassingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="9017a-161">Add plug-ins</span></span>

<span data-ttu-id="9017a-162">Hallo voor Apache Storm-topologieën die zijn geïmplementeerd in Java [Exec Maven-invoegtoepassing](http://www.mojohaus.org/exec-maven-plugin/) is nuttig omdat hiermee tooeasily Hallo topologie lokaal uitvoeren in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="9017a-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="9017a-163">Hallo na toohello toevoegen `<plugins>` sectie Hallo `pom.xml` bestand tooinclude Hallo Exec Maven-invoegtoepassing:</span><span class="sxs-lookup"><span data-stu-id="9017a-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="9017a-164">Andere nuttige invoegtoepassing is Hallo [Apache Maven-Compiler-invoegtoepassing](http://maven.apache.org/plugins/maven-compiler-plugin/), die is gebruikt toochange compilatie-opties.</span><span class="sxs-lookup"><span data-stu-id="9017a-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="9017a-165">Hallo wijzigingen Hallo Java-versie die Maven voor het Hallo-bron en doel voor uw toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9017a-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="9017a-166">Voor HDInsight __3,4 of eerder__, Hallo bron instellen en Java-versie too__1.7__ als doel.</span><span class="sxs-lookup"><span data-stu-id="9017a-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="9017a-167">Voor HDInsight __3.5__, Hallo bron instellen en Java-versie too__1.8__ als doel.</span><span class="sxs-lookup"><span data-stu-id="9017a-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="9017a-168">Toevoegen van de volgende tekst in Hallo Hallo `<plugins>` sectie Hallo `pom.xml` bestand tooinclude Hallo Apache Maven Compiler-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="9017a-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="9017a-169">In dit voorbeeld bevat 1.8, zodat Hallo doel HDInsight versie 3.5 is.</span><span class="sxs-lookup"><span data-stu-id="9017a-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="9017a-170">Resources configureren</span><span class="sxs-lookup"><span data-stu-id="9017a-170">Configure resources</span></span>

<span data-ttu-id="9017a-171">Hallo resources sectie kunt u tooinclude met niet-gecodeerde resources zoals configuratiebestanden die nodig is voor de onderdelen in Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="9017a-172">In dit voorbeeld toevoegen na de tekst in Hallo Hallo `<resources>` sectie Hallo ' bestand pom.xml.</span><span class="sxs-lookup"><span data-stu-id="9017a-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="9017a-173">In dit voorbeeld wordt Hallo resources directory in de hoofdmap Hallo van Hallo-project (`${basedir}`) als een locatie die resources bevat en omvat het Hallo-bestand met de naam `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="9017a-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="9017a-174">Dit bestand is gebruikte tooconfigure welke gegevens worden geregistreerd door Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="9017a-175">Hallo-topologie maken</span><span class="sxs-lookup"><span data-stu-id="9017a-175">Create hello topology</span></span>

<span data-ttu-id="9017a-176">Een Java gebaseerde Apache Storm-topologie bestaat uit drie onderdelen die u moet schrijven (of een verwijzing) als een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="9017a-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="9017a-177">**Spouts**: leest gegevens uit externe gegevensbronnen en verzendt gegevensstromen in Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="9017a-178">**Bolts**: voert verwerkingstaken op streams verzonden door spouts of andere bolts en verzendt een of meer stromen.</span><span class="sxs-lookup"><span data-stu-id="9017a-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="9017a-179">**Topologie**: Hiermee bepaalt u hoe Hallo spouts en bolts gerangschikte en biedt een invoerpunt voor Hallo voor Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="9017a-180">Hallo spout maken</span><span class="sxs-lookup"><span data-stu-id="9017a-180">Create hello spout</span></span>

<span data-ttu-id="9017a-181">vereisten voor het instellen van externe gegevensbronnen, tooreduce Hallo na spout verzendt gewoon willekeurig zinnen.</span><span class="sxs-lookup"><span data-stu-id="9017a-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="9017a-182">Het is een gewijzigde versie van een spout die wordt geleverd met Hallo [Storm Starter-voorbeelden](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="9017a-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="9017a-183">Zie voor een voorbeeld van een spout die uit een externe gegevensbron kan lezen, een Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="9017a-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="9017a-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): een voorbeeld spout die uit Twitter lezen</span><span class="sxs-lookup"><span data-stu-id="9017a-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="9017a-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): een spout die uit Kafka lezen</span><span class="sxs-lookup"><span data-stu-id="9017a-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="9017a-186">Maak een bestand met de naam voor Hallo-spout `RandomSentenceSpout.java` in Hallo `src\main\java\com\microsoft\example` directory en gebruik Hallo Java-code als Hallo inhoud na:</span><span class="sxs-lookup"><span data-stu-id="9017a-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="9017a-187">Hoewel deze topologie wordt slechts één spout gebruikt, kunnen andere gebruikers verschillende die gegevens uit verschillende bronnen naar de topologie Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="9017a-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="9017a-188">Hallo bolts maken</span><span class="sxs-lookup"><span data-stu-id="9017a-188">Create hello bolts</span></span>

<span data-ttu-id="9017a-189">Bolts verwerken Hallo gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="9017a-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="9017a-190">Deze topologie maakt gebruik van twee bolts:</span><span class="sxs-lookup"><span data-stu-id="9017a-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="9017a-191">**SplitSentence**: splitst Hallo zinnen gegenereerd door **RandomSentenceSpout** in afzonderlijke woorden.</span><span class="sxs-lookup"><span data-stu-id="9017a-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="9017a-192">**WordCount**: telt het aantal keren dat elk woord is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="9017a-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="9017a-193">Bolts kunnen doen alles zijn, bijvoorbeeld berekening, persistentie of tooexternal onderdelen communiceren.</span><span class="sxs-lookup"><span data-stu-id="9017a-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="9017a-194">Twee nieuwe bestanden maken `SplitSentence.java` en `WordCount.java` in Hallo `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="9017a-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="9017a-195">Gebruik Hallo tekst hello inhoud voor Hallo-bestanden te volgen:</span><span class="sxs-lookup"><span data-stu-id="9017a-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="9017a-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="9017a-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="9017a-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="9017a-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a><span data-ttu-id="9017a-198">Hallo-topologie definiëren</span><span class="sxs-lookup"><span data-stu-id="9017a-198">Define hello topology</span></span>

<span data-ttu-id="9017a-199">Hallo-topologie bindt Hallo spouts en bolts samen in een grafiek, waarmee wordt gedefinieerd hoe gegevens stromen tussen Hallo-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="9017a-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="9017a-200">Het bevat ook parallelle uitvoering hints die gebruikmaakt van Storm bij het maken van exemplaren van Hallo onderdelen binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9017a-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="9017a-201">Hallo is volgende afbeelding een eenvoudige diagram van de grafiek Hallo van onderdelen voor deze topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![diagram waarin Hallo spouts en bolts regeling](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="9017a-203">tooimplement Hallo topologie, maakt u een bestand met de naam `WordCountTopology.java` in Hallo `src\main\java\com\microsoft\example` directory.</span><span class="sxs-lookup"><span data-stu-id="9017a-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="9017a-204">Gebruik Hallo Java-code als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="9017a-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="9017a-205">Logboekregistratie configureren</span><span class="sxs-lookup"><span data-stu-id="9017a-205">Configure logging</span></span>

<span data-ttu-id="9017a-206">Storm Apache-Log4j toolog gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9017a-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="9017a-207">Als u logboekregistratie niet configureert, verzendt Hallo topologie diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9017a-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="9017a-208">toocontrol wat wordt geregistreerd, maak een bestand met de naam `log4j2.xml` in Hallo `resources` directory.</span><span class="sxs-lookup"><span data-stu-id="9017a-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="9017a-209">Gebruik hello XML als Hallo inhoud van Hallo-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="9017a-209">Use hello following XML as hello contents of hello file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="9017a-210">Deze XML configureert u een nieuwe berichtenlogboek voor Hallo `com.microsoft.example` klasse, waaronder het Hallo-onderdelen in dit voorbeeldtopologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="9017a-211">Hallo-niveau is tootrace ingesteld voor dit logboek bevat informatie die door onderdelen in deze topologie logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="9017a-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="9017a-212">Hallo `<Root level="error">` sectie configureert u Hallo hoogste niveau van logboekregistratie (alles wat u niet in `com.microsoft.example`) tooonly logboek foutgegevens.</span><span class="sxs-lookup"><span data-stu-id="9017a-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="9017a-213">Zie voor meer informatie over het configureren van logboekregistratie voor Log4j [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="9017a-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="9017a-214">Storm-versie 0.10.0 en hoger gebruiken Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="9017a-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="9017a-215">Oudere versies van storm gebruikt Log4j 1.x, die een andere indeling voor logboekbestanden-configuratie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9017a-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="9017a-216">Zie voor informatie over oudere configuratie hello, [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="9017a-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="9017a-217">Lokaal testen Hallo-topologie</span><span class="sxs-lookup"><span data-stu-id="9017a-217">Test hello topology locally</span></span>

<span data-ttu-id="9017a-218">Nadat u Hallo bestanden opslaat, gebruikt u Hallo opdracht tootest Hallo topologie lokaal te volgen.</span><span class="sxs-lookup"><span data-stu-id="9017a-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="9017a-219">Als dit wordt uitgevoerd, geeft Hallo topologie starten van de informatie.</span><span class="sxs-lookup"><span data-stu-id="9017a-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="9017a-220">Hallo is volgende tekst een voorbeeld van Hallo word aantal uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9017a-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="9017a-221">Dit voorbeeld logboek geeft aan dat woord Hallo ' en ' heeft 113 keer is verzonden.</span><span class="sxs-lookup"><span data-stu-id="9017a-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="9017a-222">Hallo blijft toogo up, zolang het Hallo-topologie wordt uitgevoerd, omdat Hallo spout continu Hallo verzendt dezelfde zinnen.</span><span class="sxs-lookup"><span data-stu-id="9017a-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="9017a-223">Er is een interval van 5 seconden tussen uitstoot van woorden en aantallen.</span><span class="sxs-lookup"><span data-stu-id="9017a-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="9017a-224">Hallo **WordCount** -onderdeel is geconfigureerd tooonly informatie verzenden wanneer een tick tuple binnenkomt.</span><span class="sxs-lookup"><span data-stu-id="9017a-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="9017a-225">Deze aanvragen die tick tuples worden alleen gedownload voor elke vijf seconden.</span><span class="sxs-lookup"><span data-stu-id="9017a-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="9017a-226">Hallo-topologie tooFlux converteren</span><span class="sxs-lookup"><span data-stu-id="9017a-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="9017a-227">Lichtstroom is een nieuw framework beschikbaar met Storm 0.10.0 en hoger, zodat u tooseparate configuratie van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="9017a-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="9017a-228">Onderdelen van uw nog steeds in Java zijn gedefinieerd, maar Hallo-topologie wordt gedefinieerd met een YAML-bestand.</span><span class="sxs-lookup"><span data-stu-id="9017a-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="9017a-229">U kunt de definitie van een standaard-topologie van het pakket met uw project, of een zelfstandig bestand gebruiken bij het indienen van Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="9017a-230">Bij het indienen van Hallo topologie tooStorm, kunt u omgevingsvariabelen of configuratiewaarden bestanden toopopulate in Hallo YAML-topologie-definitie.</span><span class="sxs-lookup"><span data-stu-id="9017a-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="9017a-231">Hallo YAML-bestand definieert Hallo onderdelen toouse voor Hallo topologie en Hallo gegevensstroom ertussen.</span><span class="sxs-lookup"><span data-stu-id="9017a-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="9017a-232">U kunt een bestand YAML opnemen als onderdeel van de jar-bestand Hallo of kunt u een extern YAML-bestand.</span><span class="sxs-lookup"><span data-stu-id="9017a-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="9017a-233">Zie voor meer informatie over lichtstroom [lichtstroom framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="9017a-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="9017a-234">Vervaldatum tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) met Storm 1.0.1, moet u mogelijk tooinstall een [Storm-ontwikkelomgeving](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun lichtstroom topologieën lokaal.</span><span class="sxs-lookup"><span data-stu-id="9017a-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="9017a-235">Hallo verplaatsen `WordCountTopology.java` bestand buiten het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="9017a-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="9017a-236">Voorheen dit bestand Hallo topologie gedefinieerd, maar met lichtstroom is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="9017a-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="9017a-237">In Hallo `resources` directory, maakt u een bestand met de naam `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="9017a-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="9017a-238">Gebruik hello tekst als Hallo inhoud van dit bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="9017a-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="9017a-239">Zorg Hallo na wijzigingen toohello `pom.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="9017a-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="9017a-240">Toevoegen van de volgende nieuwe afhankelijkheid in Hallo Hallo `<dependencies>` sectie:</span><span class="sxs-lookup"><span data-stu-id="9017a-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="9017a-241">Hallo invoegtoepassing toohello na toevoegen `<plugins>` sectie.</span><span class="sxs-lookup"><span data-stu-id="9017a-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="9017a-242">Deze invoegtoepassing Hallo maken van een pakket (jar-bestand) verwerkt voor Hallo-project en enkele specifieke tooFlux van transformaties is van toepassing bij het maken van Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="9017a-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
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
        ```

   * <span data-ttu-id="9017a-243">In Hallo **exec-maven-invoegtoepassing** `<configuration>` sectie, wijzig de waarde Hallo voor `<mainClass>` te`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="9017a-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="9017a-244">Deze instelling kan lichtstroom toohandle Hallo topologie lokaal wordt uitgevoerd in ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="9017a-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="9017a-245">In Hallo `<resources>` sectie, het toevoegen van Hallo toohello na `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="9017a-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="9017a-246">Deze XML bevat Hallo YAML-bestand dat Hallo topologie als onderdeel van het Hallo-project definieert.</span><span class="sxs-lookup"><span data-stu-id="9017a-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="9017a-247">Hallo lichtstroom topologie lokaal testen</span><span class="sxs-lookup"><span data-stu-id="9017a-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="9017a-248">Hallo toocompile na gebruik en Hallo lichtstroom topologie met behulp van Maven uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9017a-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="9017a-249">Als u met behulp van PowerShell, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9017a-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="9017a-250">Als uw Storm 1.0.1 bits wordt gebruikt, wordt deze opdracht mislukt.</span><span class="sxs-lookup"><span data-stu-id="9017a-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="9017a-251">Deze fout wordt veroorzaakt door [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="9017a-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="9017a-252">In plaats daarvan [Storm installeren in uw ontwikkelomgeving](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) en Hallo gebruik de volgende informatie.</span><span class="sxs-lookup"><span data-stu-id="9017a-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="9017a-253">Als u hebt [Storm geïnstalleerd in uw ontwikkelomgeving](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), kunt u opdrachten in plaats daarvan na Hallo:</span><span class="sxs-lookup"><span data-stu-id="9017a-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="9017a-254">Hallo `--local` parameter wordt op uw ontwikkelomgeving Hallo-topologie in de lokale modus uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9017a-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="9017a-255">Hallo `-R /topology.yaml` parameter gebruikt Hallo `topology.yaml` resource van de Hallo jar-bestand toodefine Hallo topologie van het bestand.</span><span class="sxs-lookup"><span data-stu-id="9017a-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="9017a-256">Als dit wordt uitgevoerd, geeft Hallo topologie starten van de informatie.</span><span class="sxs-lookup"><span data-stu-id="9017a-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="9017a-257">na de tekst Hello is een voorbeeld van uitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="9017a-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="9017a-258">Er is een vertraging van 10 seconden tussen batches van geregistreerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="9017a-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="9017a-259">Maak een kopie van Hallo `topology.yaml` bestand uit Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="9017a-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="9017a-260">Nieuwe bestandsnaam Hallo `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="9017a-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="9017a-261">In Hallo `newtopology.yaml` bestand, zoek Hallo volgende sectie en wijzig de waarde Hallo van `10` te`5`.</span><span class="sxs-lookup"><span data-stu-id="9017a-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="9017a-262">Deze wijziging wijzigingen hello-interval tussen het verzenden van batches van word telt van too5 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="9017a-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="9017a-263">Of als u Storm op uw ontwikkelingsomgeving hebt:</span><span class="sxs-lookup"><span data-stu-id="9017a-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="9017a-264">Wijziging Hallo `/path/to/newtopology.yaml` toohello pad toohello newtopology.yaml bestand dat u in de vorige stap Hallo hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9017a-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="9017a-265">Met deze opdracht maakt gebruik van Hallo newtopology.yaml als Hallo topologie definitie.</span><span class="sxs-lookup"><span data-stu-id="9017a-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="9017a-266">Aangezien we Hallo niet opnemen `compile` parameter Maven gebruikt Hallo-versie van Hallo project is ingebouwd in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="9017a-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="9017a-267">Eenmaal Hallo topologie begint, moet u merkt dat Hallo tijd tussen verzonden batches tooreflect Hallo waarde in newtopology.yaml is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9017a-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="9017a-268">Zo kunt u zien dat u uw configuratie via een YAML-bestand wijzigen kunt zonder toorecompile Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="9017a-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="9017a-269">Zie voor meer informatie over deze en andere functies van Hallo lichtstroom framework [lichtstroom (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="9017a-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="9017a-270">Trident</span><span class="sxs-lookup"><span data-stu-id="9017a-270">Trident</span></span>

<span data-ttu-id="9017a-271">Trident is een abstractie op hoog niveau die wordt geleverd door Storm.</span><span class="sxs-lookup"><span data-stu-id="9017a-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="9017a-272">Biedt ondersteuning voor stateful verwerking.</span><span class="sxs-lookup"><span data-stu-id="9017a-272">It supports stateful processing.</span></span> <span data-ttu-id="9017a-273">Hallo het belangrijkste voordeel van Trident is dat garanderen kunnen dat elk bericht dat Hallo topologie opgeeft slechts één keer wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="9017a-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="9017a-274">Trident gebruikt, kan uw topologie alleen garanderen dat berichten ten minste één keer worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="9017a-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="9017a-275">Er zijn ook andere verschillen, zoals de ingebouwde componenten die kunnen worden gebruikt in plaats van bolts maken.</span><span class="sxs-lookup"><span data-stu-id="9017a-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="9017a-276">Bolts zijn in feite is vervangen door minder-algemene onderdelen, zoals filters, projecties en functies.</span><span class="sxs-lookup"><span data-stu-id="9017a-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="9017a-277">Trident toepassingen kunnen worden gemaakt met behulp van Maven-projecten.</span><span class="sxs-lookup"><span data-stu-id="9017a-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="9017a-278">U hello gebruiken dezelfde basic stappen zoals eerder in dit artikel wordt beschreven, alleen Hallo code verschilt.</span><span class="sxs-lookup"><span data-stu-id="9017a-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="9017a-279">Trident kan niet ook (momenteel) worden gebruikt met Hallo lichtstroom framework.</span><span class="sxs-lookup"><span data-stu-id="9017a-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="9017a-280">Zie voor meer informatie over Trident Hallo [Trident-API-overzicht](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="9017a-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="9017a-281">Zie voor een voorbeeld van een toepassing Trident [Twitter trends onderwerpen met Apache Storm op HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="9017a-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9017a-282">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9017a-282">Next Steps</span></span>

<span data-ttu-id="9017a-283">U hebt geleerd hoe toocreate een Storm-topologie met behulp van Java.</span><span class="sxs-lookup"><span data-stu-id="9017a-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="9017a-284">Nu informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="9017a-284">Now learn how to:</span></span>

* [<span data-ttu-id="9017a-285">Implementeren en beheren van Apache Storm-topologieën op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9017a-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="9017a-286">C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9017a-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="9017a-287">U vindt meer voorbeeld Storm-topologieën in via [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9017a-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

