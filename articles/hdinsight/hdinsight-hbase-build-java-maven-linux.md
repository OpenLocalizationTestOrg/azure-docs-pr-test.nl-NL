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
# <a name="build-java-applications-for-apache-hbase"></a>Java-toepassingen voor Apache HBase bouwen

Meer informatie over hoe toocreate een [Apache HBase](http://hbase.apache.org/) toepassing in Java. Vervolgens Hallo toepassing gebruiken met HBase op Azure HDInsight.

Hallo stappen in dit document [Maven](http://maven.apache.org/) toocreate en build Hallo-project. Maven is een beheer van software-project en begrip hulpprogramma waarmee u toobuild software, documentatie en rapporten voor Java-projecten.

> [!NOTE]
> Hallo zijn stappen in dit document meest recent getest met HDInsight 3.6.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a name="requirements"></a>Vereisten

* [Java-platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 of hoger.

    > [!NOTE]
    > HDInsight 3.5 en groter vereist Java 8. Eerdere versies van HDInsight vereisen Java 7.

* [Maven](http://maven.apache.org/)

* [Een Azure HDInsight op basis van Linux-cluster met HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > Hallo stappen in dit document is getest met HDInsight-cluster versie 3.4 en 3.5. Hallo-standaardwaarden die is opgegeven in de voorbeelden zijn voor een 3.5 HDInsight-cluster.

## <a name="create-hello-project"></a>Hallo-project maken

1. Wijzig vanaf de opdrachtregel Hallo in uw ontwikkelomgeving, mappen toohello locatie waar u toocreate Hallo-project, bijvoorbeeld `cd code\hbase`.

2. Gebruik Hallo **mvn** opdracht, die is geïnstalleerd met Maven, toogenerate hello scaffolding voor Hallo-project.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > Als u met behulp van PowerShell, moet u Hallo tussen `-D` parameters tussen dubbele aanhalingstekens.
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    Met deze opdracht maakt u een map met dezelfde naam als Hallo Hallo **artefact-id** parameter (**hbaseapp** in dit voorbeeld.) Deze map bevat de volgende items Hallo:

   * **pom.XML**: Hallo Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) gegevens en configuratie details gebruikt toobuild Hallo-project bevat.
   * **SRC**: Hallo-map met de Hallo **main/java/com/microsoft/voorbeelden** directory, waar u de toepassing hello schrijven.

3. Hallo verwijderen `src/test/java/com/microsoft/examples/apptest.java` bestand. Het is niet in dit voorbeeld worden gebruikt.

## <a name="update-hello-project-object-model"></a>Hallo Project Object Model bijwerken

1. Hallo bewerken `pom.xml` bestands- en toevoegen van de volgende code in Hallo Hallo `<dependencies>` sectie:

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

    Deze sectie geeft aan dat project Hallo moet **hbase-client** en **phoenix-core** onderdelen. Tijdens het compileren worden van Hallo standaard Maven opslagplaats deze afhankelijkheden gedownload. U kunt Hallo [Maven centrale opslagplaats zoeken](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn meer informatie over deze afhankelijkheid.

   > [!IMPORTANT]
   > Hallo-versienummer van Hallo hbase-client moet overeenkomen met de Hallo-versie van HBase die beschikbaar is in uw HDInsight-cluster. Gebruik Hallo volgende tabel toofind Hallo juiste versienummer.

   | HDInsight-cluster versie | HBase versie toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3, 3.4 3.5 en 3.6 |1.1.2 |

    Zie voor meer informatie over de versies van HDInsight en -onderdelen [wat Hallo andere Hadoop-onderdelen beschikbaar met HDInsight zijn](hdinsight-component-versioning.md).

3. Hallo na code toohello toevoegen **pom.xml** bestand. Deze tekst moet binnen Hallo `<project>...</project>` labels in Hallo-bestand, bijvoorbeeld tussen `</dependencies>` en `</project>`.

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

    Deze sectie configureert u een resource (`conf/hbase-site.xml`) die configuratie-informatie voor HBase bevat.

   > [!NOTE]
   > U kunt ook configuratiewaarden via code instellen. Zie Hallo opmerkingen in Hallo `CreateTable` voorbeeld.

    Deze sectie configureert ook Hallo [Maven-Compiler-invoegtoepassing](http://maven.apache.org/plugins/maven-compiler-plugin/) en [Maven grijs-invoegtoepassing](http://maven.apache.org/plugins/maven-shade-plugin/). Hallo-compiler invoegtoepassing is gebruikte toocompile Hallo topologie. Hallo tint invoegtoepassing is gebruikte tooprevent licentie duplicatie in Hallo JAR-pakket dat wordt gebouwd door Maven. Deze invoegtoepassing gebruikte tooprevent is een fout, 'dubbele licentiebestanden' tijdens runtime op Hallo HDInsight-cluster. Met behulp van maven-schaduw-invoegtoepassing Hello `ApacheLicenseResourceTransformer` implementatie Hallo fout voorkomt.

    Hallo maven-schaduw-invoegtoepassing produceert ook een uber jar dat alle vereiste door Hallo toepassing hello afhankelijkheden bevat.

4. Hallo opslaan `pom.xml` bestand.

5. Maak een map met de naam `conf` in Hallo `hbaseapp` directory. Deze map is gebruikte toohold configuratie-informatie voor het verbinden van tooHBase.

6. Gebruik Hallo volgende opdracht toocopy hello HBase configuratie uit Hallo HBase-cluster toohello `conf` directory. Vervang `USERNAME` met Hallo-naam van uw SSH-aanmelding. Vervang `CLUSTERNAME` met de naam van uw HDInsight-cluster:

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   Voor meer informatie over het gebruik van `ssh` en `scp`, Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-hello-application"></a>Hallo-toepassing maken

1. Ga toohello `hbaseapp/src/main/java/com/microsoft/examples` map en wijzig de naam Hallo u bestand app.java te`CreateTable.java`.

2. Open Hallo `CreateTable.java` bestand en vervang de bestaande inhoud Hallo door Hallo volgende tekst:

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

    Deze code is Hallo **CreateTable** klasse, die u een tabel met de naam maakt **mensen** en deze vullen met een aantal vooraf gedefinieerde gebruikers.

3. Hallo opslaan `CreateTable.java` bestand.

4. In Hallo `hbaseapp/src/main/java/com/microsoft/examples` directory, maakt u een bestand met de naam `SearchByEmail.java`. Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:

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

    Hallo **SearchByEmail** klasse kan worden gebruikt tooquery voor rijen door e-mailadres. Omdat een filter reguliere expressie worden gebruikt, kunt u een tekenreeks of een reguliere expressie opgeven wanneer u Hallo-klasse.

5. Hallo opslaan `SearchByEmail.java` bestand.

6. In Hallo `hbaseapp/src/main/hava/com/microsoft/examples` directory, maakt u een bestand met de naam `DeleteTable.java`. Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:

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

    Deze klasse is ruimt Hallo waarvan in dit voorbeeld is gemaakt door het uitschakelen van HBase-tabellen en neer te zetten Hallo tabel gemaakt door Hallo `CreateTable` klasse.

7. Hallo opslaan `DeleteTable.java` bestand.

## <a name="build-and-package-hello-application"></a>Hallo-toepassing bouwen en pakket

1. Van Hallo `hbaseapp` map gebruik Hallo volgende opdracht toobuild een JAR-bestand dat de toepassing hello bevat:

    ```bash
    mvn clean package
    ```

    Met deze opdracht maakt en pakketten Hallo toepassing naar een JAR-bestand.

2. Wanneer Hallo-opdracht is voltooid, hello `hbaseapp/target` map bevat een bestand met de naam `hbaseapp-1.0-SNAPSHOT.jar`.

   > [!NOTE]
   > Hallo `hbaseapp-1.0-SNAPSHOT.jar` bestand is een jar uber. Deze bevat alle Hallo afhankelijkheden vereist toorun Hallo-toepassing.


## <a name="upload-hello-jar-and-run-jobs-ssh"></a>Hallo JAR uploaden en uitvoeren van taken (SSH)

Hallo na gebruik van de stappen `scp` toocopy Hallo JAR toohello primaire hoofdknooppunt van uw HBase op HDInsight-cluster. Hallo `ssh` opdracht tooconnect toohello cluster gebruikt en het Hallo-voorbeeld uitvoeren rechtstreeks op het hoofdknooppunt Hallo is.

1. tooupload hello jar toohello cluster, gebruik Hallo volgende opdracht:

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    Vervang `USERNAME` met Hallo-naam van uw SSH-aanmelding. Vervang `CLUSTERNAME` met de naam van uw HDInsight-cluster.

2. tooconnect toohello HBase-cluster gebruiken Hallo volgende opdracht:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Vervang `USERNAME` Hallo-naam van uw SSH-aanmelding. Vervang `CLUSTERNAME` met de naam van uw HDInsight-cluster.

3. een HBase-tabel met toocreate Hallo Java-toepassing, gebruik Hallo volgende opdracht:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    Deze opdracht maakt u een HBase-tabel met de naam **mensen**, en gevuld met gegevens.

4. toosearch voor e-mailadressen die zijn opgeslagen in tabel hello, gebruik Hallo volgende opdracht:

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    U ontvangt Hallo resultaten te volgen:

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. toodelete hello tabel Gebruik Hallo volgende opdracht:

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a>Uploaden van Hallo JAR-taken en uitvoeren (PowerShell)

Hallo stappen te volgen gebruik Azure PowerShell tooupload Hallo JAR toohello standaard opslag voor uw HBase-cluster. HDInsight-cmdlets worden vervolgens gebruikt toorun Hallo voorbeelden op afstand.

1. Nadat het installeren en configureren van Azure PowerShell, maakt u een bestand met de naam `hbase-runner.psm1`. Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:

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

    Dit bestand bevat twee modules:

   * **Voeg HDInsightFile** : wordt gebruikt tooupload bestanden toohello cluster
   * **Start HBaseExample** -toorun Hallo klassen eerder hebt gemaakt die wordt gebruikt

2. Hallo opslaan `hbase-runner.psm1` bestand.

3. Een nieuw Azure PowerShell-venster openen, wijzigen van mappen toohello `hbaseapp` directory, en vervolgens uitvoeren Hallo opdracht:

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    Wijzig Hallo pad toohello locatie Hallo `hbase-runner.psm1` bestand eerder hebt gemaakt. Deze opdracht wordt de module Hallo geregistreerd met Azure PowerShell.

4. Gebruik Hallo volgende opdracht tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    Vervang `hdinsightclustername` met Hallo-naam van het cluster. Hallo opdracht uploadt Hallo `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` locatie in Hallo primaire opslag voor uw cluster.

5. een tabel met toocreate Hallo `hbaseapp`, Hallo volgende opdracht gebruiken:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    Vervang `hdinsightclustername` met Hallo-naam van het cluster.

    Met deze opdracht maakt een tabel met de naam **mensen** in HBase op uw HDInsight-cluster. Met deze opdracht wordt geen uitvoer niet weergegeven in het consolevenster Hallo.

6. toosearch voor vermeldingen in de tabel hello, gebruik Hallo volgende opdracht:

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    Vervang `hdinsightclustername` met Hallo-naam van het cluster.

    Met deze opdracht maakt gebruik van Hallo `SearchByEmail` klasse toosearch voor rijen waar hello `contactinformation` kolomfamilie en Hallo `email` kolom Hallo tekenreeks bevat `contoso.com`. U ontvangt Hallo resultaten te volgen:

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    Met behulp van **fabrikam.com** voor Hallo `-emailRegex` waarde retourneert Hallo-gebruikers die hebben **fabrikam.com** in Hallo e-veld. U kunt ook reguliere expressies gebruiken als Hallo zoekterm. Bijvoorbeeld: **^ r** retourneert e-mailadressen die met een letter Hallo 'r beginnen'.

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Er zijn geen resultaten of onverwachte resultaten optreden wanneer u Start HBaseExample

Gebruik Hallo `-showErr` parameter tooview Hallo standaardfout (STDERR) dat wordt gegenereerd tijdens het Hallo-taak uitgevoerd.

## <a name="delete-hello-table"></a>Hallo-tabel verwijderen

Wanneer u klaar bent met het Hallo-voorbeeld gebruiken na toodelete Hallo Hallo **mensen** tabel die wordt gebruikt in dit voorbeeld:

__Van een `ssh` sessie__:

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

__Vanuit Azure PowerShell__:

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a>Volgende stappen

[Meer informatie over hoe toouse SQuirreL SQL met HBase](hdinsight-hbase-phoenix-squirrel-linux.md)
