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
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="e0e2b-103">Gebruik Python gebruiker gedefinieerde functies (UDF) met Hive en Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e2b-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="e0e2b-104">Meer informatie over hoe toouse Python gebruiker gedefinieerde functies (UDF) met Apache Hive en Pig in Hadoop op Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="e0e2b-105"><a name="python"></a>Python in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e2b-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="e0e2b-106">Python2.7 is standaard op HDInsight 3.0 en hoger geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="e0e2b-107">Apache Hive kan met deze versie van Python gebruikt voor de verwerking van de stroom.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="e0e2b-108">Verwerking van de stroom STDOUT en STDIN toopass van gegevens tussen Hive en Hallo UDF gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="e0e2b-109">HDInsight bevat ook Jython een Python-implementatie die is geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="e0e2b-110">Jython rechtstreeks op Hallo virtuele Java-Machine wordt uitgevoerd en maakt geen gebruik van streaming.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="e0e2b-111">Jython is Hallo Python-interpreter aanbevolen bij het gebruik van Python met Pig.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="e0e2b-112">Hallo stappen in dit document zorg Hallo veronderstellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="e0e2b-113">U maakt Hallo Python-scripts op uw lokale ontwikkelingsomgeving.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="e0e2b-114">Uploaden van Hallo scripts tooHDInsight met beide Hallo `scp` opdracht vanaf een lokale Bash-sessie of Hallo opgegeven PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="e0e2b-115">Als u wilt dat toouse hello [Azure Cloud-Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) voorbeeld toowork met HDInsight, moet u:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="e0e2b-116">Hallo-scripts in de cloudomgeving shell Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="e0e2b-117">Gebruik `scp` tooupload Hallo-bestanden van Hallo shell tooHDInsight cloud.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="e0e2b-118">Gebruik `ssh` van Hallo cloud shell tooconnect tooHDInsight en Voer Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="e0e2b-119"><a name="hivepython"></a>Hive UDF</span><span class="sxs-lookup"><span data-stu-id="e0e2b-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="e0e2b-120">Python kan worden gebruikt als een UDF van Hive via Hallo HiveQL `TRANSFORM` instructie.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="e0e2b-121">Bijvoorbeeld Hallo volgende HiveQL Hallo roept `hiveudf.py` bestand is opgeslagen in hello Azure Storage-standaardaccount voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="e0e2b-122">**HDInsight op basis van Linux**</span><span class="sxs-lookup"><span data-stu-id="e0e2b-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="e0e2b-123">**HDInsight op basis van Windows**</span><span class="sxs-lookup"><span data-stu-id="e0e2b-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="e0e2b-124">Op Windows gebaseerde HDInsight-clusters, Hallo `USING` component Hallo volledig pad toopython.exe moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="e0e2b-125">Dit is wat in dit voorbeeld doet:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-125">Here's what this example does:</span></span>

1. <span data-ttu-id="e0e2b-126">Hallo `add file` instructie aan begin Hallo van Hallo bestand voegt Hallo `hiveudf.py` bestand toohello gedistribueerde cache, zodat deze toegankelijk is voor alle knooppunten in cluster Hallo is.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="e0e2b-127">Hallo `SELECT TRANSFORM ... USING` instructie selecteert u gegevens uit Hallo `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="e0e2b-128">Dit wordt ook doorgegeven Hallo clientid, devicemake en devicemodel waarden toohello `hiveudf.py` script.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="e0e2b-129">Hallo `AS` component beschrijft Hallo velden die zijn geretourneerd door `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="e0e2b-130">Hallo hiveudf.py bestand maken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="e0e2b-131">Maak een tekstbestand met de naam op uw ontwikkelomgeving `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="e0e2b-132">Gebruik Hallo code als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="e0e2b-133">Dit script voert Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="e0e2b-134">Een line-of gegevens lezen uit STDIN.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="e0e2b-135">Hallo-regelteken afsluitende wordt verwijderd met behulp van `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="e0e2b-136">Bij het uitvoeren van de verwerking van de stroom bevat een enkele regel alle Hallo waarden met een teken tabblad tussen elke waarde.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="e0e2b-137">Dus `string.split(line, "\t")` gebruikte toosplit Hallo invoer op elk tabblad retourneren alleen Hallo-velden kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="e0e2b-138">Bij het verwerken is voltooid, moet Hallo uitvoer worden geschreven tooSTDOUT als één regel, met een tabblad tussen elk veld.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="e0e2b-139">Bijvoorbeeld `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="e0e2b-140">Hallo `while` lus wordt herhaald totdat Nee `line` lezen is.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="e0e2b-141">Hallo-scriptuitvoer is een samenvoeging van de invoerwaarden Hallo voor `devicemake` en `devicemodel`, en een hash van Hallo samengevoegd waarde.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="e0e2b-142">Zie [uitgevoerd Hallo voorbeelden](#running) voor het toorun in dit voorbeeld op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="e0e2b-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="e0e2b-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="e0e2b-144">Een pythonscript kan worden gebruikt als een UDF van Pig via Hallo `GENERATE` instructie.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="e0e2b-145">U kunt met behulp van Jython of C Python Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="e0e2b-146">Jython wordt uitgevoerd op Hallo JVM en systeemeigen kan worden aangeroepen vanuit Pig.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="e0e2b-147">Python C is een extern proces Hallo gegevens van Pig op Hallo JVM wordt verzonden toohello script dat wordt uitgevoerd in een Python-proces.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="e0e2b-148">Hallo-uitvoer van Hallo Python-script wordt verzonden naar Pig.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="e0e2b-149">toospecify hello Python-interpreter, gebruik `register` bij verwijzingen naar Hallo pythonscript.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="e0e2b-150">Hallo volgende voorbeelden registreren scripts met Pig als `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="e0e2b-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="e0e2b-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="e0e2b-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="e0e2b-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e2b-153">Wanneer u Jython, Hallo pad toohello pig_jython bestand is mogelijk een lokaal pad of een WASB: / / pad.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="e0e2b-154">Echter, wanneer u C Python gebruikt, u moet verwijzen naar een bestand op het lokale bestandssysteem Hallo van Hallo-knooppunt dat u van toosubmit Hallo Pig-taak gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="e0e2b-155">Zodra de vorige registratie, Hallo Pig Latin voor dit voorbeeld is Hallo dezelfde voor beide:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="e0e2b-156">Dit is wat in dit voorbeeld doet:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-156">Here's what this example does:</span></span>

1. <span data-ttu-id="e0e2b-157">de eerste regel Hallo Hallo voorbeeldgegevensbestand, laadt `sample.log` in `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="e0e2b-158">Ook wordt gedefinieerd hoe elke record als een `chararray`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="e0e2b-159">de volgende regel Hallo gefilterd met een null-waarden voor het opslaan van Hallo resultaat van Hallo-bewerking in `LOG`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="e0e2b-160">Vervolgens wordt een iteratie over Hallo-records in `LOG` en maakt gebruik van `GENERATE` tooinvoke hello `create_structure` methode opgenomen in Hallo Python/Jython script geladen als `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="e0e2b-161">`LINE`gebruikte toopass is Hallo huidige record toohello functie.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="e0e2b-162">Ten slotte Hallo uitgangen zijn gedumpte tooSTDOUT met Hallo `DUMP` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="e0e2b-163">Deze opdracht geeft Hallo resultaten nadat Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="e0e2b-164">Hallo pigudf.py bestand maken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="e0e2b-165">Maak een tekstbestand met de naam op uw ontwikkelomgeving `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="e0e2b-166">Gebruik Hallo code als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-166">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="e0e2b-167">In Hallo Pig Latin voorbeeld hebben we Hallo gedefinieerd `LINE` ingevoerd als een chararray omdat er geen consistente schema voor Hallo-invoer is.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="e0e2b-168">Hallo pythonscript transformeert Hallo gegevens in een consistente schema voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="e0e2b-169">Hallo `@outputSchema` instructie Hallo-indeling van Hallo-gegevens die worden geretourneerd tooPig definieert.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="e0e2b-170">In dit geval heeft een **gegevens eigenschappenverzameling**, namelijk een Pig-gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="e0e2b-171">Hallo eigenschappenverzameling bevat Hallo velden, dit allemaal chararray (tekenreeksen zijn) te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="e0e2b-172">datum - hello datum Hallo logboekvermelding is gemaakt</span><span class="sxs-lookup"><span data-stu-id="e0e2b-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="e0e2b-173">tijd - Hallo Hallo logboekvermelding is gemaakt</span><span class="sxs-lookup"><span data-stu-id="e0e2b-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="e0e2b-174">ClassName - Hallo klasse NaamVermelding Hallo is gemaakt voor</span><span class="sxs-lookup"><span data-stu-id="e0e2b-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="e0e2b-175">Level - Hallo logboekniveau</span><span class="sxs-lookup"><span data-stu-id="e0e2b-175">level - hello log level</span></span>
   * <span data-ttu-id="e0e2b-176">detail - uitgebreide gegevens voor Hallo logboekvermelding</span><span class="sxs-lookup"><span data-stu-id="e0e2b-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="e0e2b-177">Vervolgens Hallo `def create_structure(input)` definieert Hallo-functie die Pig regel items die moeten worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="e0e2b-178">Hallo bijvoorbeeld gegevens `sample.log`, voornamelijk voldoet toohello datum, tijd, classname, niveau, toegelicht en we willen tooreturn schema.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="e0e2b-179">Het document bevat echter een paar regels die met beginnen `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="e0e2b-180">Deze regels moet gewijzigde toomatch Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="e0e2b-181">Hallo `if` voor deze instructie wordt gecontroleerd en vervolgens massages Hallo invoergegevens toomove hello `*java.lang.Exception*` tekenreeks toohello hiertoe Hallo gegevens in de regel met het schema van de verwachte uitvoer te brengen.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="e0e2b-182">Vervolgens Hallo `split` opdracht gebruikte toosplit Hallo data-at-Hallo eerste vier tekens is.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="e0e2b-183">Hallo-uitvoer is toegewezen in `date`, `time`, `classname`, `level`, en `detail`.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="e0e2b-184">Hallo-waarden worden ten slotte tooPig geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="e0e2b-185">Hallo gegevens wordt tooPig geretourneerd, heeft een consistente schema zoals gedefinieerd in Hallo `@outputSchema` instructie.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="e0e2b-186"><a name="running"></a>Uploaden en Voer Hallo-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e0e2b-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e2b-187">Hallo **SSH** stappen werken alleen met een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e0e2b-188">Hallo **PowerShell** stappen werken met een Linux- of Windows gebaseerde HDInsight-cluster, maar vereisen dat een Windows-client.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="e0e2b-189">SSH</span><span class="sxs-lookup"><span data-stu-id="e0e2b-189">SSH</span></span>

<span data-ttu-id="e0e2b-190">Zie voor meer informatie over het gebruik van SSH [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e0e2b-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="e0e2b-191">Gebruik `scp` toocopy Hallo bestanden tooyour HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="e0e2b-192">Bijvoorbeeld, Hallo na de opdracht kopieën Hallo bestanden tooa cluster met de naam **mijncluster**.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="e0e2b-193">SSH tooconnect toohello cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="e0e2b-194">Hallo SSH-sessie, toevoegen Hallo python bestanden geüpload eerder toohello WASB opslagruimte voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="e0e2b-195">Gebruik Hallo volgende stappen na het uploaden van bestanden Hallo toorun Hallo Hive en Pig-taken.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="e0e2b-196">Hallo UDF Hive gebruiken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="e0e2b-197">Gebruik Hallo `hive` opdrachtshell toostart Hallo hive.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="e0e2b-198">U ziet een `hive>` vragen nadat Hallo shell is geladen.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="e0e2b-199">Voer Hallo volgende query op Hallo `hive>` prompt:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="e0e2b-200">Na het invoeren van de laatste regel Hallo Hallo-taak moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="e0e2b-201">Zodra het Hallo-taak is voltooid, retourneert deze uitvoer vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="e0e2b-202">Hallo UDF Pig gebruiken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="e0e2b-203">Gebruik Hallo `pig` toostart Hallo opdrachtshell.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="e0e2b-204">U ziet een `grunt>` vragen nadat Hallo shell is geladen.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="e0e2b-205">Voer Hallo volgende instructies uit op Hallo `grunt>` prompt:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="e0e2b-206">Na het invoeren van Hallo volgt regel Hallo-taak moet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="e0e2b-207">Zodra het Hallo-taak is voltooid, retourneert deze uitvoer vergelijkbare toohello volgt gegevens:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="e0e2b-208">Gebruik `quit` tooexit Hallo knorvis shell en gebruik vervolgens Hallo tooedit hello pigudf.py bestand op het lokale bestandssysteem hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="e0e2b-209">Eenmaal in de editor Hallo Opmerking verwijderen Hallo volgt regel door het verwijderen van Hallo `#` teken vanaf het begin van regel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="e0e2b-210">Zodra het Hallo wijziging is aangebracht, gebruikt u Ctrl + X tooexit Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="e0e2b-211">Selecteer Y en voer vervolgens toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="e0e2b-212">Gebruik Hallo `pig` opdrachtshell toostart Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="e0e2b-213">Zodra u zich op Hallo `grunt>` gevraagd, gebruikt u Hallo toorun Hallo pythonscript met Hallo C Python-interpreter te volgen.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="e0e2b-214">Zodra deze taak is voltooid, ziet u Hallo dezelfde uitvoer als wanneer u Hallo-script met behulp van Jython eerder is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="e0e2b-215">PowerShell: Bestanden voor uploaden Hallo</span><span class="sxs-lookup"><span data-stu-id="e0e2b-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="e0e2b-216">U kunt PowerShell tooupload Hallo bestanden toohello HDInsight-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="e0e2b-217">Hallo scriptbestanden tooupload Hallo Python volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e0e2b-218">Hallo stappen in deze sectie Azure PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="e0e2b-219">Zie voor meer informatie over het gebruik van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0e2b-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

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
> <span data-ttu-id="e0e2b-220">Wijziging Hallo `C:\path\to` waarde toohello pad toohello bestanden op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="e0e2b-221">Dit script wordt informatie opgehaald voor uw HDInsight-cluster en vervolgens pakt Hallo-account en -sleutel voor het standaardopslagaccount hello en uploads Hallo bestanden toohello hoofdmap van Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e2b-222">Zie voor meer informatie over het uploaden van bestanden Hallo [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md) document.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="e0e2b-223">PowerShell: Hallo UDF Hive gebruiken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="e0e2b-224">PowerShell kan ook worden gebruikt tooremotely uitvoeren Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="e0e2b-225">Gebruik Hallo volgende PowerShell-script toorun een Hive-query die gebruikmaakt van **hiveudf.py** script:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0e2b-226">Voordat u, Hallo script wordt u gevraagd Hallo HTTPs/Admin accountgegevens voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

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

<span data-ttu-id="e0e2b-227">uitvoer voor Hallo Hallo **Hive** taak moet worden weergegeven vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="e0e2b-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="e0e2b-228">Pig (Jython)</span></span>

<span data-ttu-id="e0e2b-229">PowerShell kan ook worden gebruikt toorun Pig Latin taken.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="e0e2b-230">een taak Pig Latin die gebruikmaakt van Hallo toorun **pigudf.py** script, Hallo volgende PowerShell-script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="e0e2b-231">Wanneer een taak met PowerShell op afstand wordt verzonden, is mogelijk toouse C Python niet als Hallo interpreter.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

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

<span data-ttu-id="e0e2b-232">uitvoer voor Hallo Hallo **Pig** taak moet worden weergegeven vergelijkbaar toohello gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="e0e2b-233"><a name="troubleshooting"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="e0e2b-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="e0e2b-234">Fout bij het uitvoeren van taken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-234">Errors when running jobs</span></span>

<span data-ttu-id="e0e2b-235">Wanneer Hallo hive-taak wordt uitgevoerd, kan een vergelijkbare toohello na de tekst van fout optreden:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="e0e2b-236">Dit probleem kan worden veroorzaakt door Hallo regeleinden in Hallo Python-bestand.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="e0e2b-237">Veel Windows editors standaard toousing CRLF als Hallo regel die eindigt, maar meestal verwachten LF Linux-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="e0e2b-238">U kunt de volgende PowerShell-instructies tooremove Hallo CR tekens voordat u uploadt Hallo bestand tooHDInsight hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="e0e2b-239">PowerShell-scripts</span><span class="sxs-lookup"><span data-stu-id="e0e2b-239">PowerShell scripts</span></span>

<span data-ttu-id="e0e2b-240">Beide Hallo voorbeeld PowerShell-scripts gebruiken toorun Hallo voorbeelden bevatten een opmerkingen regel die de foutuitvoer voor Hallo-taak wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="e0e2b-241">Als u Hallo verwachte uitvoer voor Hallo-taak niet ziet, verwijder de opmerking Hallo volgende regel en zien als de informatie over de fout Hallo duidt op een probleem.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="e0e2b-242">Hallo foutinformatie (STDERR) en Hallo resultaat van taak hello (STDOUT) zijn eveneens geregistreerde tooyour HDInsight-opslag.</span><span class="sxs-lookup"><span data-stu-id="e0e2b-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="e0e2b-243">Voor deze taak...</span><span class="sxs-lookup"><span data-stu-id="e0e2b-243">For this job...</span></span> | <span data-ttu-id="e0e2b-244">Deze bestanden in de blob-container Hallo bekijken</span><span class="sxs-lookup"><span data-stu-id="e0e2b-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="e0e2b-245">Hive</span><span class="sxs-lookup"><span data-stu-id="e0e2b-245">Hive</span></span> |<span data-ttu-id="e0e2b-246">/ HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="e0e2b-246">/HivePython/stderr</span></span><p><span data-ttu-id="e0e2b-247">/ HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="e0e2b-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="e0e2b-248">Pig</span><span class="sxs-lookup"><span data-stu-id="e0e2b-248">Pig</span></span> |<span data-ttu-id="e0e2b-249">/ PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="e0e2b-249">/PigPython/stderr</span></span><p><span data-ttu-id="e0e2b-250">/ PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="e0e2b-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="e0e2b-251"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0e2b-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="e0e2b-252">Als u tooload Python-modules die standaard zijn niet beschikbaar moet, Zie [hoe een module tooAzure HDInsight toodeploy](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0e2b-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="e0e2b-253">Zie voor andere manieren toouse Pig, Hive en toolearn over het gebruik van MapReduce, Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="e0e2b-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="e0e2b-254">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e2b-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e0e2b-255">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e2b-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e0e2b-256">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e0e2b-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
