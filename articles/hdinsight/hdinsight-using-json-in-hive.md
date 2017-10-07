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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Verwerken en analyseren van JSON-documenten met Hive in HDInsight

Meer informatie over hoe tooprocess JSON-bestanden met Hive in HDInsight en analyseren. Hallo JSON-document te volgen wordt in Hallo zelfstudie gebruikt:

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

Hallo-bestand kan worden gevonden op wasb://processjson@hditutorialdata.blob.core.windows.net/. Zie voor meer informatie over het gebruik van Azure Blob storage met HDInsight [HDFS-compatibele Azure Blob storage gebruiken met Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md). U kunt kopiëren Hallo bestand toohello standaardcontainer van uw cluster.

In deze zelfstudie gebruikt u Hallo Hive-console.  Zie voor instructies Hallo Hive-console te openen, [Hive gebruiken met Hadoop op HDInsight met extern bureaublad](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>JSON-documenten plat
Hallo-methoden die worden vermeld in de volgende sectie Hallo vereisen Hallo JSON-document in één rij. U moet dus Hallo JSON-document tooa tekenreeks afvlakken. Als uw JSON-document al afgevlakt is, kunt u deze stap overslaan en gaat u de volgende sectie rechte toohello analyseren JSON-gegevens.

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

Hallo onbewerkte JSON-bestand bevindt zich op  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Hallo *StudentsRaw* Hive-tabel verwijst toohello onbewerkte samenvoegen JSON-document.

Hallo *StudentsOneLine* Hive-tabel Hallo-gegevens opslaat in HDInsight standaardbestandssysteem onder Hallo Hallo */json/studenten/* pad.

de instructie INSERT Hallo vult Hallo StudentOneLine tabel met Hallo afgevlakt JSON-gegevens.

Hallo SELECT-instructie wordt slechts één rij retourneren.

Dit is de uitvoer Hallo Hallo SELECT-instructie:

![Plat van Hallo JSON-document.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>JSON-documenten in Hive analyseren
Hive biedt drie verschillende mechanismen toorun query's op JSON-documenten:

* Gebruik Hallo GET\_JSON\_OBJECT UDF (door de gebruiker gedefinieerde functie)
* Hallo JSON_TUPLE UDF gebruiken
* Gebruik aangepaste serde-schrijfbewerking
* schrijven dat van jou UDF met Python of andere talen. Zie [in dit artikel] [ hdinsight-python] op uw eigen Python-code die worden uitgevoerd met Hive.

### <a name="use-hello-getjsonobject-udf"></a>Gebruik Hallo GET\_JSON_OBJECT UDF
Hive biedt een ingebouwde UDF aangeroepen [json-object ophalen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), die JSON opvragen tijdens runtime kunt uitvoeren. Deze methode heeft twee argumenten – Hallo-tabelnaam en de methodenaam is Hallo platte JSON-document en Hallo JSON veld die toobe geparseerd behoeften. Bekijk een voorbeeld toosee de werking van deze UDF.

Hallo-voornaam en achternaam op voor elke student ophalen

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Hier volgt Hallo uitvoer wanneer deze query wordt uitgevoerd in het consolevenster.

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

Er zijn enkele beperkingen van Hallo get-json_object UDF.

* Omdat elk veld in de query Hallo Hallo query reparsing is vereist, maar dit invloed op Hallo prestaties.
* OPHALEN van\_JSON_OBJECT() Hallo tekenreeksweergave van een matrix retourneert. tooconvert deze matrix tooa Hive-matrix, hebt u toouse reguliere expressies tooreplace vierkante haken Hallo ' [' en ']' en vervolgens ook aanroep tooget Hallo matrix verdeeld.

Daarom Hallo Hive wiki raadt json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Hallo JSON_TUPLE UDF gebruiken
Een andere UDF geleverd door Hive heet [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), uitvoert, wordt er beter dan [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Deze methode heeft een set van sleutels en een JSON-tekenreeks en retourneert een tuple van waarden met een functie. Hallo retourneert volgende query Hallo student-id en de Hallo hoogwaardige van Hallo JSON-document:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

Hallo-uitvoer van dit script in Hallo Hive-console:

![json_tuple UDF][image-hdi-hivejson-jsontuple]

JSON\_TUPLE gebruikt Hallo [lateral weergave](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntaxis in Hive, waardoor json\_tuple toocreate een virtuele tabel door toe te passen Hallo UDT functie tooeach rij van de oorspronkelijke tabel Hallo.  Complexe JSONs onhandig te vanwege Hallo herhaald gebruik van LATERALE weergave. JSON_TUPLE kan bovendien geneste JSONs niet verwerken.

### <a name="use-custom-serde"></a>Gebruik aangepaste serde-schrijfbewerking
Serde-schrijfbewerking is de beste keuze Hallo voor het parseren van geneste JSON-documenten, kunt u toodefine Hallo JSON-schema en gebruik Hallo schema tooparse Hallo documenten. In deze zelfstudie maakt u een Hallo populairder serde-schrijfbewerking die is ontwikkeld door [Roberto Congiu](https://github.com/rcongiu).

**toouse Hallo aangepaste serde-schrijfbewerking:**

1. Installeer [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Hallo Windows X64-versie van Hallo JDK kiezen als u met behulp van de implementatie van Windows hello van HDInsight toobe gaat
   
   > [!WARNING]
   > 1.8 JDK werkt niet met deze serde-schrijfbewerking.
   > 
   > 
   
    Nadat het Hallo-installatie is voltooid, Voeg een nieuwe omgevingsvariabele:
   
   1. Open **weergave Geavanceerde systeeminstellingen** van Windows-welkomstscherm.
   2. Klik op **omgevingsvariabelen**.  
   3. Voeg een nieuwe **JAVA_HOME** omgevingsvariabele te wijst**C:\Program Files\Java\jdk1.7.0_55** of waar uw JDK is geïnstalleerd.
      
      ![Instellen van de juiste configuratiewaarden voor JDK][image-hdi-hivejson-jdk]
2. Installeer [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Hallo bin mappad tooyour toevoegen door te gaan tooControl Configuratiescherm--> bewerken Hallo systeemvariabelen voor uw account omgevingsvariabelen. Hallo volgende schermafbeelding ziet u hoe toodo dit.
   
    ![Maven instellen][image-hdi-hivejson-maven]
3. Kloon Hallo-project uit [Hive-JSON-serde-schrijfbewerking](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github-site. U kunt dit doen door te klikken op 'Zip downloaden' Hallo-knop, zoals wordt weergegeven in de volgende schermafbeelding Hallo.
   
    ![Hallo project klonen][image-hdi-hivejson-serde]

4: Ga toohello map waar u dit pakket en 'mvn pakket' hebt gedownload. Dit moet Hallo nodig jar-bestanden die u vervolgens via toohello cluster kopiëren kunt maken.

5: Ga toohello doelmap onder de hoofdmap Hallo waar u Hallo pakket hebt gedownload. Upload Hallo json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar bestand toohead-knooppunt van uw cluster. Ik heb meestal gezet onder Hallo hive binaire map: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin of iets soortgelijks.

6: Typ '/path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar jar toevoegen' in hello hive-prompt. Omdat in mijn geval Hallo jar in Hallo C:\apps\dist\hive-0.13.x\bin map, kan ik Hallo jar met Hallo naam zoals rechtstreeks toevoegen:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![JAR tooyour project toe te voegen][image-hdi-hivejson-addjar]

U bent nu klaar toouse hello serde-schrijfbewerking toorun query's op Hallo JSON-document.

Hallo-instructie maakt een tabel met een gedefinieerd schema:

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

toolist hello voornaam en achternaam van Hallo studenten

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Hier volgt Hallo resultaat van Hallo Hive-console.

![Serde-schrijfbewerking Query 1][image-hdi-hivejson-serde_query1]

toocalculate hello som van scores van Hallo JSON-document

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Hallo voorgaande query gebruikt [laterale weergave vouwen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand Hallo matrix van scores zodat ze kunnen worden opgeteld.

Hier volgt Hallo-uitvoer van Hallo Hive-console.

![Serde-schrijfbewerking Query 2][image-hdi-hivejson-serde_query2]

toofind die een bepaalde student heeft meer dan 80 punten berekend:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Hallo voorgaande query retourneert een matrix Hive in tegenstelling tot get\_json\_-object, dat een tekenreeks retourneert.

![Serde-schrijfbewerking Query 3][image-hdi-hivejson-serde_query3]

Als u wilt dat tooskil onjuist gevormd JSON, klikt u vervolgens als uiteengezet in Hallo [wiki-pagina](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) van deze serde-schrijfbewerking kunt u die bereiken door Hallo na de code in te voeren:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Samenvatting
Tot slot Hallo type JSON-operator in component die u kiest is afhankelijk van uw scenario. Als u een eenvoudige JSON-document hebt en u hoeft alleen één veld toolook up op – kunt u toouse Hallo Hive UDF get\_json\_object. Als u meer dan één sleutel toolook up op hebt, kunt u json_tuple gebruiken. Als u een geneste document hebt, moet u Hallo JSON serde-schrijfbewerking gebruiken.

## <a name="next-steps"></a>Volgende stappen

Zie voor andere verwante artikelen

* [Hive en HiveQL gebruiken met Hadoop in HDInsight tooanalyze een voorbeeldbestand van de Apache-log4j](hdinsight-use-hive.md)
* [Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Twitter-gegevens met Hive in HDInsight analyseren](hdinsight-analyze-twitter-data.md)
* [Voer een met behulp van Azure DB die Cosmos en HDInsight Hadoop](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
