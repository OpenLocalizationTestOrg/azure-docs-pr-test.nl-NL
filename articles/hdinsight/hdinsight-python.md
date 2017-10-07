---
title: aaaPython UDF met Apache Hive en Pig - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Python gebruiker gedefinieerde functies (UDF) van Hive en Pig in HDInsight worden Hadoop-technologie Hallo stack in Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Gebruik Python gebruiker gedefinieerde functies (UDF) met Hive en Pig in HDInsight

Meer informatie over hoe toouse Python gebruiker gedefinieerde functies (UDF) met Apache Hive en Pig in Hadoop op Azure HDInsight.

## <a name="python"></a>Python in HDInsight

Python2.7 is standaard op HDInsight 3.0 en hoger geïnstalleerd. Apache Hive kan met deze versie van Python gebruikt voor de verwerking van de stroom. Verwerking van de stroom STDOUT en STDIN toopass van gegevens tussen Hive en Hallo UDF gebruikt.

HDInsight bevat ook Jython een Python-implementatie die is geschreven in Java. Jython rechtstreeks op Hallo virtuele Java-Machine wordt uitgevoerd en maakt geen gebruik van streaming. Jython is Hallo Python-interpreter aanbevolen bij het gebruik van Python met Pig.

> [!WARNING]
> Hallo stappen in dit document zorg Hallo veronderstellingen te volgen: 
>
> * U maakt Hallo Python-scripts op uw lokale ontwikkelingsomgeving.
> * Uploaden van Hallo scripts tooHDInsight met beide Hallo `scp` opdracht vanaf een lokale Bash-sessie of Hallo opgegeven PowerShell-script.
>
> Als u wilt dat toouse hello [Azure Cloud-Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) voorbeeld toowork met HDInsight, moet u:
>
> * Hallo-scripts in de cloudomgeving shell Hallo maken.
> * Gebruik `scp` tooupload Hallo-bestanden van Hallo shell tooHDInsight cloud.
> * Gebruik `ssh` van Hallo cloud shell tooconnect tooHDInsight en Voer Hallo voorbeelden.

## <a name="hivepython"></a>Hive UDF

Python kan worden gebruikt als een UDF van Hive via Hallo HiveQL `TRANSFORM` instructie. Bijvoorbeeld Hallo volgende HiveQL Hallo roept `hiveudf.py` bestand is opgeslagen in hello Azure Storage-standaardaccount voor Hallo-cluster.

**HDInsight op basis van Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight op basis van Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> Op Windows gebaseerde HDInsight-clusters, Hallo `USING` component Hallo volledig pad toopython.exe moet opgeven.

Dit is wat in dit voorbeeld doet:

1. Hallo `add file` instructie aan begin Hallo van Hallo bestand voegt Hallo `hiveudf.py` bestand toohello gedistribueerde cache, zodat deze toegankelijk is voor alle knooppunten in cluster Hallo is.
2. Hallo `SELECT TRANSFORM ... USING` instructie selecteert u gegevens uit Hallo `hivesampletable`. Dit wordt ook doorgegeven Hallo clientid, devicemake en devicemodel waarden toohello `hiveudf.py` script.
3. Hallo `AS` component beschrijft Hallo velden die zijn geretourneerd door `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Hallo hiveudf.py bestand maken


Maak een tekstbestand met de naam op uw ontwikkelomgeving `hiveudf.py`. Gebruik Hallo code als Hallo inhoud van Hallo-bestand te volgen:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Dit script voert Hallo van de volgende activiteiten:

1. Een line-of gegevens lezen uit STDIN.
2. Hallo-regelteken afsluitende wordt verwijderd met behulp van `string.strip(line, "\n ")`.
3. Bij het uitvoeren van de verwerking van de stroom bevat een enkele regel alle Hallo waarden met een teken tabblad tussen elke waarde. Dus `string.split(line, "\t")` gebruikte toosplit Hallo invoer op elk tabblad retourneren alleen Hallo-velden kunnen worden.
4. Bij het verwerken is voltooid, moet Hallo uitvoer worden geschreven tooSTDOUT als één regel, met een tabblad tussen elk veld. Bijvoorbeeld `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Hallo `while` lus wordt herhaald totdat Nee `line` lezen is.

Hallo-scriptuitvoer is een samenvoeging van de invoerwaarden Hallo voor `devicemake` en `devicemodel`, en een hash van Hallo samengevoegd waarde.

Zie [uitgevoerd Hallo voorbeelden](#running) voor het toorun in dit voorbeeld op uw HDInsight-cluster.

## <a name="pigpython"></a>Pig UDF

Een pythonscript kan worden gebruikt als een UDF van Pig via Hallo `GENERATE` instructie. U kunt met behulp van Jython of C Python Hallo-script uitvoeren.

* Jython wordt uitgevoerd op Hallo JVM en systeemeigen kan worden aangeroepen vanuit Pig.
* Python C is een extern proces Hallo gegevens van Pig op Hallo JVM wordt verzonden toohello script dat wordt uitgevoerd in een Python-proces. Hallo-uitvoer van Hallo Python-script wordt verzonden naar Pig.

toospecify hello Python-interpreter, gebruik `register` bij verwijzingen naar Hallo pythonscript. Hallo volgende voorbeelden registreren scripts met Pig als `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Wanneer u Jython, Hallo pad toohello pig_jython bestand is mogelijk een lokaal pad of een WASB: / / pad. Echter, wanneer u C Python gebruikt, u moet verwijzen naar een bestand op het lokale bestandssysteem Hallo van Hallo-knooppunt dat u van toosubmit Hallo Pig-taak gebruikmaakt.

Zodra de vorige registratie, Hallo Pig Latin voor dit voorbeeld is Hallo dezelfde voor beide:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Dit is wat in dit voorbeeld doet:

1. de eerste regel Hallo Hallo voorbeeldgegevensbestand, laadt `sample.log` in `LOGS`. Ook wordt gedefinieerd hoe elke record als een `chararray`.
2. de volgende regel Hallo gefilterd met een null-waarden voor het opslaan van Hallo resultaat van Hallo-bewerking in `LOG`.
3. Vervolgens wordt een iteratie over Hallo-records in `LOG` en maakt gebruik van `GENERATE` tooinvoke hello `create_structure` methode opgenomen in Hallo Python/Jython script geladen als `myfuncs`. `LINE`gebruikte toopass is Hallo huidige record toohello functie.
4. Ten slotte Hallo uitgangen zijn gedumpte tooSTDOUT met Hallo `DUMP` opdracht. Deze opdracht geeft Hallo resultaten nadat Hallo-bewerking is voltooid.

### <a name="create-hello-pigudfpy-file"></a>Hallo pigudf.py bestand maken

Maak een tekstbestand met de naam op uw ontwikkelomgeving `pigudf.py`. Gebruik Hallo code als Hallo inhoud van Hallo-bestand te volgen:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

In Hallo Pig Latin voorbeeld hebben we Hallo gedefinieerd `LINE` ingevoerd als een chararray omdat er geen consistente schema voor Hallo-invoer is. Hallo pythonscript transformeert Hallo gegevens in een consistente schema voor uitvoer.

1. Hallo `@outputSchema` instructie Hallo-indeling van Hallo-gegevens die worden geretourneerd tooPig definieert. In dit geval heeft een **gegevens eigenschappenverzameling**, namelijk een Pig-gegevenstype. Hallo eigenschappenverzameling bevat Hallo velden, dit allemaal chararray (tekenreeksen zijn) te volgen:

   * datum - hello datum Hallo logboekvermelding is gemaakt
   * tijd - Hallo Hallo logboekvermelding is gemaakt
   * ClassName - Hallo klasse NaamVermelding Hallo is gemaakt voor
   * Level - Hallo logboekniveau
   * detail - uitgebreide gegevens voor Hallo logboekvermelding

2. Vervolgens Hallo `def create_structure(input)` definieert Hallo-functie die Pig regel items die moeten worden doorgegeven.

3. Hallo bijvoorbeeld gegevens `sample.log`, voornamelijk voldoet toohello datum, tijd, classname, niveau, toegelicht en we willen tooreturn schema. Het document bevat echter een paar regels die met beginnen `*java.lang.Exception*`. Deze regels moet gewijzigde toomatch Hallo schema. Hallo `if` voor deze instructie wordt gecontroleerd en vervolgens massages Hallo invoergegevens toomove hello `*java.lang.Exception*` tekenreeks toohello hiertoe Hallo gegevens in de regel met het schema van de verwachte uitvoer te brengen.

4. Vervolgens Hallo `split` opdracht gebruikte toosplit Hallo data-at-Hallo eerste vier tekens is. Hallo-uitvoer is toegewezen in `date`, `time`, `classname`, `level`, en `detail`.

5. Hallo-waarden worden ten slotte tooPig geretourneerd.

Hallo gegevens wordt tooPig geretourneerd, heeft een consistente schema zoals gedefinieerd in Hallo `@outputSchema` instructie.

## <a name="running"></a>Uploaden en Voer Hallo-voorbeelden

> [!IMPORTANT]
> Hallo **SSH** stappen werken alleen met een Linux gebaseerde HDInsight-cluster. Hallo **PowerShell** stappen werken met een Linux- of Windows gebaseerde HDInsight-cluster, maar vereisen dat een Windows-client.

### <a name="ssh"></a>SSH

Zie voor meer informatie over het gebruik van SSH [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Gebruik `scp` toocopy Hallo bestanden tooyour HDInsight-cluster. Bijvoorbeeld, Hallo na de opdracht kopieën Hallo bestanden tooa cluster met de naam **mijncluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. SSH tooconnect toohello cluster gebruiken.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Hallo SSH-sessie, toevoegen Hallo python bestanden geüpload eerder toohello WASB opslagruimte voor Hallo-cluster.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Gebruik Hallo volgende stappen na het uploaden van bestanden Hallo toorun Hallo Hive en Pig-taken.

#### <a name="use-hello-hive-udf"></a>Hallo UDF Hive gebruiken

1. Gebruik Hallo `hive` opdrachtshell toostart Hallo hive. U ziet een `hive>` vragen nadat Hallo shell is geladen.

2. Voer Hallo volgende query op Hallo `hive>` prompt:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Na het invoeren van de laatste regel Hallo Hallo-taak moet worden gestart. Zodra het Hallo-taak is voltooid, retourneert deze uitvoer vergelijkbare toohello voorbeeld te volgen:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Hallo UDF Pig gebruiken

1. Gebruik Hallo `pig` toostart Hallo opdrachtshell. U ziet een `grunt>` vragen nadat Hallo shell is geladen.

2. Voer Hallo volgende instructies uit op Hallo `grunt>` prompt:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Na het invoeren van Hallo volgt regel Hallo-taak moet worden gestart. Zodra het Hallo-taak is voltooid, retourneert deze uitvoer vergelijkbare toohello volgt gegevens:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Gebruik `quit` tooexit Hallo knorvis shell en gebruik vervolgens Hallo tooedit hello pigudf.py bestand op het lokale bestandssysteem hello te volgen:

    ```bash
    nano pigudf.py
    ```

5. Eenmaal in de editor Hallo Opmerking verwijderen Hallo volgt regel door het verwijderen van Hallo `#` teken vanaf het begin van regel Hallo Hallo:

    ```bash
    #from pig_util import outputSchema
    ```

    Zodra het Hallo wijziging is aangebracht, gebruikt u Ctrl + X tooexit Hallo-editor. Selecteer Y en voer vervolgens toosave Hallo wijzigingen.

6. Gebruik Hallo `pig` opdrachtshell toostart Hallo opnieuw. Zodra u zich op Hallo `grunt>` gevraagd, gebruikt u Hallo toorun Hallo pythonscript met Hallo C Python-interpreter te volgen.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Zodra deze taak is voltooid, ziet u Hallo dezelfde uitvoer als wanneer u Hallo-script met behulp van Jython eerder is uitgevoerd.

### <a name="powershell-upload-hello-files"></a>PowerShell: Bestanden voor uploaden Hallo

U kunt PowerShell tooupload Hallo bestanden toohello HDInsight-server gebruiken. Hallo scriptbestanden tooupload Hallo Python volgende gebruiken:

> [!IMPORTANT] 
> Hallo stappen in deze sectie Azure PowerShell gebruiken. Zie voor meer informatie over het gebruik van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Wijziging Hallo `C:\path\to` waarde toohello pad toohello bestanden op uw ontwikkelomgeving.

Dit script wordt informatie opgehaald voor uw HDInsight-cluster en vervolgens pakt Hallo-account en -sleutel voor het standaardopslagaccount hello en uploads Hallo bestanden toohello hoofdmap van Hallo-container.

> [!NOTE]
> Zie voor meer informatie over het uploaden van bestanden Hallo [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md) document.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: Hallo UDF Hive gebruiken

PowerShell kan ook worden gebruikt tooremotely uitvoeren Hive-query's. Gebruik Hallo volgende PowerShell-script toorun een Hive-query die gebruikmaakt van **hiveudf.py** script:

> [!IMPORTANT]
> Voordat u, Hallo script wordt u gevraagd Hallo HTTPs/Admin accountgegevens voor uw HDInsight-cluster.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

uitvoer voor Hallo Hallo **Hive** taak moet worden weergegeven vergelijkbaar toohello voorbeeld te volgen:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell kan ook worden gebruikt toorun Pig Latin taken. een taak Pig Latin die gebruikmaakt van Hallo toorun **pigudf.py** script, Hallo volgende PowerShell-script gebruiken:

> [!NOTE]
> Wanneer een taak met PowerShell op afstand wordt verzonden, is mogelijk toouse C Python niet als Hallo interpreter.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

uitvoer voor Hallo Hallo **Pig** taak moet worden weergegeven vergelijkbaar toohello gegevens te volgen:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="errors-when-running-jobs"></a>Fout bij het uitvoeren van taken

Wanneer Hallo hive-taak wordt uitgevoerd, kan een vergelijkbare toohello na de tekst van fout optreden:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Dit probleem kan worden veroorzaakt door Hallo regeleinden in Hallo Python-bestand. Veel Windows editors standaard toousing CRLF als Hallo regel die eindigt, maar meestal verwachten LF Linux-toepassingen.

U kunt de volgende PowerShell-instructies tooremove Hallo CR tekens voordat u uploadt Hallo bestand tooHDInsight hello gebruiken:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>PowerShell-scripts

Beide Hallo voorbeeld PowerShell-scripts gebruiken toorun Hallo voorbeelden bevatten een opmerkingen regel die de foutuitvoer voor Hallo-taak wordt weergegeven. Als u Hallo verwachte uitvoer voor Hallo-taak niet ziet, verwijder de opmerking Hallo volgende regel en zien als de informatie over de fout Hallo duidt op een probleem.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Hallo foutinformatie (STDERR) en Hallo resultaat van taak hello (STDOUT) zijn eveneens geregistreerde tooyour HDInsight-opslag.

| Voor deze taak... | Deze bestanden in de blob-container Hallo bekijken |
| --- | --- |
| Hive |/ HivePython/stderr<p>/ HivePython/stdout |
| Pig |/ PigPython/stderr<p>/ PigPython/stdout |

## <a name="next"></a>Volgende stappen

Als u tooload Python-modules die standaard zijn niet beschikbaar moet, Zie [hoe een module tooAzure HDInsight toodeploy](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Zie voor andere manieren toouse Pig, Hive en toolearn over het gebruik van MapReduce, Hallo documenten te volgen:

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)
