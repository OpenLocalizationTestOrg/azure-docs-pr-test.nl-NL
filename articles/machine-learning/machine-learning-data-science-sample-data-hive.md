---
title: aaaSample gegevens in Azure HDInsight Hive-tabellen | Microsoft Docs
description: Omlaag steekproef nemen van gegevens in Azure HDInsight (Hadopop) Hive-tabellen
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Voorbeeldgegevens in Hive-tabellen in Azure HDInsight
In dit artikel wordt beschreven hoe toodown-voorbeeldgegevens opgeslagen in Azure HDInsight Hive-tabellen met Hive-query's. We hebben betrekking op dit gebruikte steekproeven op drie manieren:

* Uniform steekproeven
* Steekproeven door groepen
* Toepassing stratificatie steekproeven

Hallo volgende **menu** koppelingen tootopics waarin wordt beschreven hoe toosample gegevens uit verschillende omgevingen voor opslag.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Waarom een steekproef nemen uit uw gegevens?**
Als u van plan bent tooanalyze Hallo-gegevensset te groot is, is het meestal een goed idee Hallo toodown-sample data tooreduce het tooa kleiner, maar representatief en gemakkelijker grootte. Dit vereenvoudigt het begrip van de gegevens, exploratie en functie-engineering. De rol in Hallo Team gegevens wetenschappelijke processen is tooenable snel maken van een prototype van Hallo gegevensverwerking functies en machine learning-modellen.

Deze taak steekproeven is een stap in Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Hoe toosubmit Hive-query's
Hive-query's kunnen worden verzonden in Hallo Hadoop-opdrachtregel-console op Hallo hoofdknooppunt van Hallo Hadoop-cluster. toodo dit, meld u aan bij de hoofdknooppunt Hallo van Hallo Hadoop-cluster, opent u Hallo Hadoop-opdrachtregel-console, en het Hallo Hive-query's van daaruit verzenden. Zie voor instructies voor het indienen van Hive-query's in de Hadoop-opdrachtregel-console Hallo [hoe tooSubmit Hive-query's](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a>Uniform steekproeven
Uniform steekproeven betekent dat elke rij in de gegevensset Hallo evenveel kans wordt door actieve heeft. Dit kan worden geïmplementeerd door een extra veld ASELECT() toohello-gegevensset toe te voegen in binnenste 'select' Hallo-query en Hallo in buitenste 'select'-query die voorwaarde op dat willekeurige veld.

Hier volgt een voorbeeldquery:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

Hier `<sample rate, 0-1>` Hallo deel van de records die gebruikers Hallo toosample wilt bevat.

## <a name="group"></a>Steekproeven door groepen
Wanneer steekproeven categorische gegevens, kunt u wordt tooeither opnemen of uitsluiten van alle exemplaren van een bepaalde waarde van een variabele categorische Hallo. Dit is wat door 'steekproeven per groep'.
Bijvoorbeeld als er een categorische variabele 'Status', die waarden NY, MA, CA, NJ, PA, enzovoort, u wilt dat records Hallo dezelfde status worden altijd samen, of ze of niet worden vastgelegd.

Hier volgt een voorbeeldquery die voorbeelden per groep:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Toepassing stratificatie steekproeven
Steekproeven van toepassing is stratificatie met opzicht tooa categorische variabele wanneer Hallo voorbeelden verkregen waarden van dat categorische hebben die zich in Hallo dezelfde verhouding zoals in Hallo bovenliggende populatie van welke Hallo voorbeelden zijn verkregen. Met behulp van Hallo hetzelfde voorbeeld zoals hierboven, Stel dat uw gegevens altijd onderliggende populaties door statussen, spreek NJ 100 waarnemingen heeft, NY is 60 opmerkingen en WA is 300 opmerkingen. Als u Hallo frequentie van opgeeft toepassing stratificatie steekproeven toobe 0,5 vervolgens hello voorbeeld verkregen moet hebben ongeveer 50, 30 en 150 opmerkingen van NJ NY en WA respectievelijk.

Hier volgt een voorbeeldquery:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Zie voor meer informatie over meer geavanceerde steekproeven methoden die beschikbaar in de component zijn [LanguageManual steekproeven](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

