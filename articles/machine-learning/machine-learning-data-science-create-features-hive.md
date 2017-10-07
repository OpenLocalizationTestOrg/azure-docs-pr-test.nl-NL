---
title: functies voor gegevens in een Hadoop-cluster met behulp van Hive-query's aaaCreate | Microsoft Docs
description: Voorbeelden van Hive-query's die functies in de gegevens die zijn opgeslagen in een Azure HDInsight Hadoop-cluster genereren.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Met Hive-query’s functies maken voor gegevens in een Hadoop-cluster
Dit document ziet u hoe de functies toocreate voor gegevens wordt opgeslagen in een Azure HDInsight Hadoop-cluster met behulp van Hive-query's. Deze Hive-query gebruikt ingesloten Hive gebruiker gedefinieerde functies (UDF's), Hallo scripts die worden geleverd.

Hallo bewerkingen die nodig zijn toocreate functies kunnen geheugenintensief zijn. Hallo-prestaties van Hive-query's wordt meer kritieke in dergelijke gevallen en kan worden verbeterd door het afstemmen van bepaalde parameters. Hallo afstemming van deze parameters wordt besproken in het laatste gedeelte Hallo.

Voorbeelden van Hallo-query's die worden aangeboden zijn specifieke toohello [NYC Taxi reis gegevens](http://chriswhong.com/open-data/foil_nyc_taxi/) scenario's zijn ook beschikbaar [GitHub-opslagplaats](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Deze query's al gegevensschema dat is opgegeven en zijn gereed toobe verzonden toorun. In het laatste gedeelte hello, worden ook parameters die gebruikers afstemmen kunnen zodat Hallo prestaties van Hive-query's kunnen worden verbeterd besproken.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Dit **menu** koppelingen tootopics waarin wordt beschreven hoe toocreate functies voor gegevens in verschillende omgevingen. Deze taak is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt:

* Een Azure storage-account gemaakt. Als u instructies nodig hebt, raadpleegt u [een Azure Storage-account maken](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Een aangepaste Hadoop-cluster met Hallo HDInsight-service wordt ingericht.  Als u instructies nodig hebt, raadpleegt u [aanpassen Azure HDInsight Hadoop-Clusters voor geavanceerde analyses](machine-learning-data-science-customize-hadoop-cluster.md).
* Hallo-gegevens zijn geüpload tooHive tabellen in Azure HDInsight Hadoop-clusters. Als dit niet het geval is, voert u [maken en de belasting tooHive gegevenstabellen](machine-learning-data-science-move-hive-tables.md) tooupload gegevens tooHive eerst tabellen.
* Externe toegang toohello cluster ingeschakeld. Als u instructies nodig hebt, raadpleegt u [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Functie generatie
In deze sectie vindt u enkele voorbeelden van Hallo manieren waarin functies kunnen genereren met behulp van Hive-query's. Nadat u extra functies hebt gegenereerd, kunt u hen toevoegen als kolommen toohello bestaande tabel of een nieuwe tabel maken met de Hallo extra functies en primaire sleutel, die vervolgens kan worden samengevoegd met de oorspronkelijke tabel Hallo. Hier volgen voorbeelden Hallo:

1. [De frequentie op basis van functie generatie](#hive-frequencyfeature)
2. [Risico's van Categorische variabelen in binaire classificatie](#hive-riskfeature)
3. [Functies van Datetime Field uitpakken](#hive-datefeatures)
4. [Functies van tekstveld uitpakken](#hive-textfeatures)
5. [Afstand tussen GPS-coördinaten berekenen](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>De frequentie op basis van functie generatie
Is het vaak nuttig toocalculate Hallo frequenties van Hallo niveaus van een categorische variabele of Hallo frequenties van bepaalde combinaties van niveaus uit meerdere categorische variabelen. Gebruikers kunnen Hallo script toocalculate na deze frequenties gebruiken:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Risico's van Categorische variabelen in binaire classificatie
In binaire indeling moeten we tooconvert niet-numerieke categorische variabelen in de numerieke onderdelen waarbinnen Hallo modellen wordt alleen gebruikt numerieke functies worden uitgevoerd. Dit wordt gedaan door elk niet-numerieke niveau vervangen door een numerieke risico. In deze sectie laten we zien sommige algemene Hive-query's die Hallo risico waarden (logboek kans) van een variabele categorische berekenen.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

In dit voorbeeld variabelen `smooth_param1` en `smooth_param2` zijn toosmooth Hallo risico waarden berekend op basis van Hallo-gegevens. Risico's hebben een bereik tussen -Inf en inf-bestand. Een risico's > 0 geeft aan dat Hallo waarschijnlijkheid dat doel Hallo gelijk too1 groter dan 0,5 is.

Nadat het Hallo risico tabel wordt berekend, kunnen gebruikers risico waarden tooa tabel lid maakt van met de Hallo risico tabel toewijzen. gekoppelde Hallo Hive-query is opgegeven in de vorige sectie.

### <a name="hive-datefeatures"></a>Functies van Datetime-Fields uitpakken
Hive wordt geleverd met een reeks UDF's voor het verwerken van datetime-velden. In Hive, is het Hallo-standaardnotatie voor datum/tijd is jjjj-MM-dd 00:00:00 ' ('01-01-1970 12:21:32 ' bijvoorbeeld). In deze sectie laten we zien voorbeelden die dag van een maand, de maand van een datetime-veld Hallo Hallo uitpakken en andere voorbeelden die een datum/tijd-tekenreeks in een indeling geconverteerd andere dan Hallo standaard tooa datetime indelingstekenreeks opmaken in standaard.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Deze Hive-query wordt ervan uitgegaan dat Hallo *&#60; datetime-veld >* Hallo standaard datum/tijd-indeling.

Als een datetime-veld niet in de standaardindeling hello is, u tooconvert Hallo datetime-veld in Unix tijdstempel eerst moet en vervolgens converteren Hallo Unix tijd stempel tooa datetime tekenreeks die is standaard Hallo indeling. Wanneer Hallo datetime in standaard indeling is, kunnen gebruikers Hallo ingesloten datetime UDF's tooextract functies toepassen.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

In deze query als hello *&#60; datetime-veld >* heeft Hallo patroon zoals *03/26/2015 12:04:39*, Hallo *' &#60; patroon van Hallo datetime-veld >'* moet `'MM/dd/yyyy HH:mm:ss'`. tootest, gebruikers kunnen uitvoeren

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Hallo *hivesampletable* in deze query vooraf is geïnstalleerd op alle Azure HDInsight Hadoop-clusters standaard wanneer Hallo clusters zijn ingericht.

### <a name="hive-textfeatures"></a>Functies van tekstvelden uitpakken
Wanneer Hallo Hive-tabel een tekstveld die een tekenreeks met woorden die worden gescheiden door spaties bevat heeft, haalt hello volgende query Hallo-lengte van tekenreeks Hallo en Hallo aantal woorden in Hallo-tekenreeks.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Afstand tussen sets GPS-coördinaten berekenen
Hallo-query is opgegeven in deze sectie kan rechtstreeks toegepaste toohello NYC Taxi reis gegevens zijn. Hallo-doel van deze query is tooshow hoe tooapply ingesloten wiskundige functies in Hive toogenerate onderdelen.

Hallo velden die worden gebruikt in deze query zijn Hallo GPS-coördinaten van ophalen en dropoff locaties, met de naam *ophalen\_lengtegraad*, *ophalen\_breedtegraad*,  *dropoff\_lengtegraad*, en *dropoff\_breedtegraad*. Hallo-query's die direct afstand tussen Hallo ophalen en dropoff coördinaten Hallo berekenen zijn:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

Hallo wiskundige vergelijkingen die Hallo afstand tussen twee GPS-coördinaten berekenen vindt u op Hallo <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">MovableType Scripts</a> geschreven door Peter Lapisu-site. Hallo in diens Javascript functie `toRad()` is zojuist *lat_or_lon*pi/180 *, die graden tooradians converteert. Hier *lat_or_lon* Hallo breedtegraad of lengtegraad is. Aangezien Hive geen Hallo functie biedt `atan2`, maar biedt Hallo functie `atan`, Hallo `atan2` functie wordt geïmplementeerd door `atan` functie in Hallo hierboven Hive-query met Hallo definitie is opgegeven in <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Werkruimte maken](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Een volledige lijst met Hive ingesloten UDF's u in Hallo vinden kunnen **ingebouwde functies** sectie op Hallo <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Onderwerpen over geavanceerde: stemmen Hive Parameters tooImprove Query snelheid
Hallo standaardparameter instellingen van Hive-cluster niet mogelijk geschikt voor Hallo Hive-query's en Hallo-gegevens die Hallo query's worden verwerkt. In deze sectie bespreken we een aantal parameters die gebruikers kunnen afstemmen Hallo prestaties van Hive-query's verbeteren. Gebruikers moeten tooadd Hallo parameter afstemmen van query's voordat Hallo query's van het verwerken van gegevens.

1. **Java-heap ruimte**: voor query's met betrekking tot lid te worden grote gegevenssets of verwerken van lange records **bijna vol heap** is een algemene fout Hallo. Dit door het instellen van de parameters kan worden afgestemd *mapreduce.map.java.opts* en *mapreduce.task.io.sort.mb* toodesired waarden. Hier volgt een voorbeeld:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Deze parameter wordt 4GB geheugen tooJava heap ruimte en maakt ook sorteren efficiënter door meer geheugen toewijzen voor het. Als er een taak mislukt fouten gerelateerde tooheap ruimte is een goed idee tooplay met deze toewijzingen.

1. **DFS-blokgrootte** : deze parameter stelt Hallo kleinste gegevenseenheid die Hallo system bestandsopslag. Bijvoorbeeld als Hallo DFS-blokgrootte 128MB is, wordt geen gegevens van de grootte van minder dan en omhoog in too128MB opgeslagen in één blok, terwijl de gegevens die groter is dan 128MB extra blokken wordt toegewezen. Het kiezen van een zeer kleine blokgrootte zorgt ervoor dat grote overhead in Hadoop omdat Hallo naam knooppunt tooprocess veel meer aanvragen toofind Hallo relevante blok met toohello bestand betrekking heeft. Een aanbevolen instelling als betreft gigabyte (of groter) gegevens:
   
        set dfs.block.size=128m;
2. **Join-bewerking in Hive optimaliseren** : terwijl joinbewerkingen in Hallo kaart/verminderen framework doorgaans plaatsvinden in Hallo verminderen soms fase, enorm veel toeneemt kunnen worden bereikt door het plannen van joins in Hallo kaart fase (ook wel 'mapjoins' genoemd). toodirect Hive toodo dit zo veel mogelijk we kunt instellen:
   
        set hive.auto.convert.join=true;
3. **Aantal mappers tooHive Hallo geven** : terwijl Hadoop kunnen Hallo gebruiker tooset Hallo aantal verkleiningstoestellen, Hallo aantal mappers is doorgaans niet worden ingesteld door de gebruiker Hallo. Een truc waarmee bepaalde mate van controle op dit nummer is toochoose hello Hadoop variabelen *mapred.min.split.size* en *mapred.max.split.size* als Hallo grootte van elke kaart taak wordt bepaald door:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Normaal gesproken Hallo standaardwaarde van *mapred.min.split.size* is ingesteld op 0 van *mapred.max.split.size* is **Long.MAX** , evenals *dfs.block.size* is 64MB. Zoals we zien, gegevensgrootte van het gegeven Hallo afstemming van deze parameters door 'instelling' ze kunt u ons tootune Hallo aantal mappers gebruikt.
4. Enkele andere meer **geavanceerde opties voor** voor het optimaliseren van Hive prestaties hieronder worden vermeld. Dit kunnen u tooset Hallo toegewezen geheugen toomap taken verminderen en nuttig kunnen zijn bij het afstemmen van de prestaties. Houd er rekening mee dat Hallo *mapreduce.reduce.memory.mb* mag niet groter dan de grootte van fysiek geheugen Hallo van elk knooppunt van de werknemer in Hallo Hadoop-cluster.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

