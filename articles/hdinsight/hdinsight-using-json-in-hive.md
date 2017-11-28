---
title: aaaAnalyze en proces JSON-documenten met Hive in HDInsight | Microsoft Docs
description: Ontdek hoe toouse JSON-documenten en analyseer ze met Hive in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="6df14-103">Verwerken en analyseren van JSON-documenten met Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6df14-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="6df14-104">Meer informatie over hoe tooprocess JSON-bestanden met Hive in HDInsight en analyseren.</span><span class="sxs-lookup"><span data-stu-id="6df14-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="6df14-105">Hallo JSON-document te volgen wordt in Hallo zelfstudie gebruikt:</span><span class="sxs-lookup"><span data-stu-id="6df14-105">hello following JSON document is used in hello tutorial:</span></span>

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

<span data-ttu-id="6df14-106">Hallo-bestand kan worden gevonden op wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="6df14-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="6df14-107">Zie voor meer informatie over het gebruik van Azure Blob storage met HDInsight [HDFS-compatibele Azure Blob storage gebruiken met Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6df14-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="6df14-108">U kunt kopiëren Hallo bestand toohello standaardcontainer van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6df14-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="6df14-109">In deze zelfstudie gebruikt u Hallo Hive-console.</span><span class="sxs-lookup"><span data-stu-id="6df14-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="6df14-110">Zie voor instructies Hallo Hive-console te openen, [Hive gebruiken met Hadoop op HDInsight met extern bureaublad](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="6df14-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="6df14-111">JSON-documenten plat</span><span class="sxs-lookup"><span data-stu-id="6df14-111">Flatten JSON documents</span></span>
<span data-ttu-id="6df14-112">Hallo-methoden die worden vermeld in de volgende sectie Hallo vereisen Hallo JSON-document in één rij.</span><span class="sxs-lookup"><span data-stu-id="6df14-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="6df14-113">U moet dus Hallo JSON-document tooa tekenreeks afvlakken.</span><span class="sxs-lookup"><span data-stu-id="6df14-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="6df14-114">Als uw JSON-document al afgevlakt is, kunt u deze stap overslaan en gaat u de volgende sectie rechte toohello analyseren JSON-gegevens.</span><span class="sxs-lookup"><span data-stu-id="6df14-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

<span data-ttu-id="6df14-115">Hallo onbewerkte JSON-bestand bevindt zich op  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="6df14-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="6df14-116">Hallo *StudentsRaw* Hive-tabel verwijst toohello onbewerkte samenvoegen JSON-document.</span><span class="sxs-lookup"><span data-stu-id="6df14-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="6df14-117">Hallo *StudentsOneLine* Hive-tabel Hallo-gegevens opslaat in HDInsight standaardbestandssysteem onder Hallo Hallo */json/studenten/* pad.</span><span class="sxs-lookup"><span data-stu-id="6df14-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="6df14-118">de instructie INSERT Hallo vult Hallo StudentOneLine tabel met Hallo afgevlakt JSON-gegevens.</span><span class="sxs-lookup"><span data-stu-id="6df14-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="6df14-119">Hallo SELECT-instructie wordt slechts één rij retourneren.</span><span class="sxs-lookup"><span data-stu-id="6df14-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="6df14-120">Dit is de uitvoer Hallo Hallo SELECT-instructie:</span><span class="sxs-lookup"><span data-stu-id="6df14-120">Here is hello output of hello SELECT statement:</span></span>

![Plat van Hallo JSON-document.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="6df14-122">JSON-documenten in Hive analyseren</span><span class="sxs-lookup"><span data-stu-id="6df14-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="6df14-123">Hive biedt drie verschillende mechanismen toorun query's op JSON-documenten:</span><span class="sxs-lookup"><span data-stu-id="6df14-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="6df14-124">Gebruik Hallo GET\_JSON\_OBJECT UDF (door de gebruiker gedefinieerde functie)</span><span class="sxs-lookup"><span data-stu-id="6df14-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="6df14-125">Hallo JSON_TUPLE UDF gebruiken</span><span class="sxs-lookup"><span data-stu-id="6df14-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="6df14-126">Gebruik aangepaste serde-schrijfbewerking</span><span class="sxs-lookup"><span data-stu-id="6df14-126">use custom SerDe</span></span>
* <span data-ttu-id="6df14-127">schrijven dat van jou UDF met Python of andere talen.</span><span class="sxs-lookup"><span data-stu-id="6df14-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="6df14-128">Zie [in dit artikel] [ hdinsight-python] op uw eigen Python-code die worden uitgevoerd met Hive.</span><span class="sxs-lookup"><span data-stu-id="6df14-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="6df14-129">Gebruik Hallo GET\_JSON_OBJECT UDF</span><span class="sxs-lookup"><span data-stu-id="6df14-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="6df14-130">Hive biedt een ingebouwde UDF aangeroepen [json-object ophalen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), die JSON opvragen tijdens runtime kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6df14-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="6df14-131">Deze methode heeft twee argumenten – Hallo-tabelnaam en de methodenaam is Hallo platte JSON-document en Hallo JSON veld die toobe geparseerd behoeften.</span><span class="sxs-lookup"><span data-stu-id="6df14-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="6df14-132">Bekijk een voorbeeld toosee de werking van deze UDF.</span><span class="sxs-lookup"><span data-stu-id="6df14-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="6df14-133">Hallo-voornaam en achternaam op voor elke student ophalen</span><span class="sxs-lookup"><span data-stu-id="6df14-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="6df14-134">Hier volgt Hallo uitvoer wanneer deze query wordt uitgevoerd in het consolevenster.</span><span class="sxs-lookup"><span data-stu-id="6df14-134">Here is hello output when running this query in console window.</span></span>

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="6df14-136">Er zijn enkele beperkingen van Hallo get-json_object UDF.</span><span class="sxs-lookup"><span data-stu-id="6df14-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="6df14-137">Omdat elk veld in de query Hallo Hallo query reparsing is vereist, maar dit invloed op Hallo prestaties.</span><span class="sxs-lookup"><span data-stu-id="6df14-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="6df14-138">OPHALEN van\_JSON_OBJECT() Hallo tekenreeksweergave van een matrix retourneert.</span><span class="sxs-lookup"><span data-stu-id="6df14-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="6df14-139">tooconvert deze matrix tooa Hive-matrix, hebt u toouse reguliere expressies tooreplace vierkante haken Hallo ' [' en ']' en vervolgens ook aanroep tooget Hallo matrix verdeeld.</span><span class="sxs-lookup"><span data-stu-id="6df14-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="6df14-140">Daarom Hallo Hive wiki raadt json_tuple.</span><span class="sxs-lookup"><span data-stu-id="6df14-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="6df14-141">Hallo JSON_TUPLE UDF gebruiken</span><span class="sxs-lookup"><span data-stu-id="6df14-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="6df14-142">Een andere UDF geleverd door Hive heet [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), uitvoert, wordt er beter dan [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="6df14-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="6df14-143">Deze methode heeft een set van sleutels en een JSON-tekenreeks en retourneert een tuple van waarden met een functie.</span><span class="sxs-lookup"><span data-stu-id="6df14-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="6df14-144">Hallo retourneert volgende query Hallo student-id en de Hallo hoogwaardige van Hallo JSON-document:</span><span class="sxs-lookup"><span data-stu-id="6df14-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="6df14-145">Hallo-uitvoer van dit script in Hallo Hive-console:</span><span class="sxs-lookup"><span data-stu-id="6df14-145">hello output of this script in hello Hive console:</span></span>

![json_tuple UDF][image-hdi-hivejson-jsontuple]

<span data-ttu-id="6df14-147">JSON\_TUPLE gebruikt Hallo [lateral weergave](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntaxis in Hive, waardoor json\_tuple toocreate een virtuele tabel door toe te passen Hallo UDT functie tooeach rij van de oorspronkelijke tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="6df14-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="6df14-148">Complexe JSONs onhandig te vanwege Hallo herhaald gebruik van LATERALE weergave.</span><span class="sxs-lookup"><span data-stu-id="6df14-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="6df14-149">JSON_TUPLE kan bovendien geneste JSONs niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="6df14-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="6df14-150">Gebruik aangepaste serde-schrijfbewerking</span><span class="sxs-lookup"><span data-stu-id="6df14-150">Use custom SerDe</span></span>
<span data-ttu-id="6df14-151">Serde-schrijfbewerking is de beste keuze Hallo voor het parseren van geneste JSON-documenten, kunt u toodefine Hallo JSON-schema en gebruik Hallo schema tooparse Hallo documenten.</span><span class="sxs-lookup"><span data-stu-id="6df14-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="6df14-152">In deze zelfstudie maakt u een Hallo populairder serde-schrijfbewerking die is ontwikkeld door [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="6df14-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="6df14-153">**toouse Hallo aangepaste serde-schrijfbewerking:**</span><span class="sxs-lookup"><span data-stu-id="6df14-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="6df14-154">Installeer [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="6df14-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="6df14-155">Hallo Windows X64-versie van Hallo JDK kiezen als u met behulp van de implementatie van Windows hello van HDInsight toobe gaat</span><span class="sxs-lookup"><span data-stu-id="6df14-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="6df14-156">1.8 JDK werkt niet met deze serde-schrijfbewerking.</span><span class="sxs-lookup"><span data-stu-id="6df14-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="6df14-157">Nadat het Hallo-installatie is voltooid, Voeg een nieuwe omgevingsvariabele:</span><span class="sxs-lookup"><span data-stu-id="6df14-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="6df14-158">Open **weergave Geavanceerde systeeminstellingen** van Windows-welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="6df14-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="6df14-159">Klik op **omgevingsvariabelen**.</span><span class="sxs-lookup"><span data-stu-id="6df14-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="6df14-160">Voeg een nieuwe **JAVA_HOME** omgevingsvariabele te wijst**C:\Program Files\Java\jdk1.7.0_55** of waar uw JDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6df14-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Instellen van de juiste configuratiewaarden voor JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="6df14-162">Installeer [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="6df14-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="6df14-163">Hallo bin mappad tooyour toevoegen door te gaan tooControl Configuratiescherm--> bewerken Hallo systeemvariabelen voor uw account omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="6df14-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="6df14-164">Hallo volgende schermafbeelding ziet u hoe toodo dit.</span><span class="sxs-lookup"><span data-stu-id="6df14-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Maven instellen][image-hdi-hivejson-maven]
3. <span data-ttu-id="6df14-166">Kloon Hallo-project uit [Hive-JSON-serde-schrijfbewerking](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github-site.</span><span class="sxs-lookup"><span data-stu-id="6df14-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="6df14-167">U kunt dit doen door te klikken op 'Zip downloaden' Hallo-knop, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="6df14-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Hallo project klonen][image-hdi-hivejson-serde]

<span data-ttu-id="6df14-169">4: Ga toohello map waar u dit pakket en 'mvn pakket' hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="6df14-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="6df14-170">Dit moet Hallo nodig jar-bestanden die u vervolgens via toohello cluster kopiëren kunt maken.</span><span class="sxs-lookup"><span data-stu-id="6df14-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="6df14-171">5: Ga toohello doelmap onder de hoofdmap Hallo waar u Hallo pakket hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="6df14-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="6df14-172">Upload Hallo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar bestand toohead-knooppunt van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6df14-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="6df14-173">Ik heb meestal gezet onder Hallo hive binaire map: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin of iets soortgelijks.</span><span class="sxs-lookup"><span data-stu-id="6df14-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="6df14-174">6: Typ '/path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar jar toevoegen' in hello hive-prompt.</span><span class="sxs-lookup"><span data-stu-id="6df14-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="6df14-175">Omdat in mijn geval Hallo jar in Hallo C:\apps\dist\hive-0.13.x\bin map, kan ik Hallo jar met Hallo naam zoals rechtstreeks toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6df14-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![JAR tooyour project toe te voegen][image-hdi-hivejson-addjar]

<span data-ttu-id="6df14-177">U bent nu klaar toouse hello serde-schrijfbewerking toorun query's op Hallo JSON-document.</span><span class="sxs-lookup"><span data-stu-id="6df14-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="6df14-178">Hallo-instructie maakt een tabel met een gedefinieerd schema:</span><span class="sxs-lookup"><span data-stu-id="6df14-178">hello following statement creates a table with a defined schema:</span></span>

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

<span data-ttu-id="6df14-179">toolist hello voornaam en achternaam van Hallo studenten</span><span class="sxs-lookup"><span data-stu-id="6df14-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="6df14-180">Hier volgt Hallo resultaat van Hallo Hive-console.</span><span class="sxs-lookup"><span data-stu-id="6df14-180">Here is hello result from hello Hive console.</span></span>

![Serde-schrijfbewerking Query 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="6df14-182">toocalculate hello som van scores van Hallo JSON-document</span><span class="sxs-lookup"><span data-stu-id="6df14-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="6df14-183">Hallo voorgaande query gebruikt [laterale weergave vouwen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand Hallo matrix van scores zodat ze kunnen worden opgeteld.</span><span class="sxs-lookup"><span data-stu-id="6df14-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="6df14-184">Hier volgt Hallo-uitvoer van Hallo Hive-console.</span><span class="sxs-lookup"><span data-stu-id="6df14-184">Here is hello output from hello Hive console.</span></span>

![Serde-schrijfbewerking Query 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="6df14-186">toofind die een bepaalde student heeft meer dan 80 punten berekend:</span><span class="sxs-lookup"><span data-stu-id="6df14-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="6df14-187">Hallo voorgaande query retourneert een matrix Hive in tegenstelling tot get\_json\_-object, dat een tekenreeks retourneert.</span><span class="sxs-lookup"><span data-stu-id="6df14-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Serde-schrijfbewerking Query 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="6df14-189">Als u wilt dat tooskil onjuist gevormd JSON, klikt u vervolgens als uiteengezet in Hallo [wiki-pagina](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) van deze serde-schrijfbewerking kunt u die bereiken door Hallo na de code in te voeren:</span><span class="sxs-lookup"><span data-stu-id="6df14-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="6df14-190">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6df14-190">Summary</span></span>
<span data-ttu-id="6df14-191">Tot slot Hallo type JSON-operator in component die u kiest is afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="6df14-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="6df14-192">Als u een eenvoudige JSON-document hebt en u hoeft alleen één veld toolook up op – kunt u toouse Hallo Hive UDF get\_json\_object.</span><span class="sxs-lookup"><span data-stu-id="6df14-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="6df14-193">Als u meer dan één sleutel toolook up op hebt, kunt u json_tuple gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6df14-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="6df14-194">Als u een geneste document hebt, moet u Hallo JSON serde-schrijfbewerking gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6df14-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6df14-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6df14-195">Next steps</span></span>

<span data-ttu-id="6df14-196">Zie voor andere verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="6df14-196">For other related articles, see</span></span>

* [<span data-ttu-id="6df14-197">Hive en HiveQL gebruiken met Hadoop in HDInsight tooanalyze een voorbeeldbestand van de Apache-log4j</span><span class="sxs-lookup"><span data-stu-id="6df14-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6df14-198">Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6df14-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="6df14-199">Twitter-gegevens met Hive in HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="6df14-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="6df14-200">Voer een met behulp van Azure DB die Cosmos en HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="6df14-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
