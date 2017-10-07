---
title: aaaExtend U-SQL-scripts met behulp van Python in Azure Data Lake Analytics | Microsoft Docs
description: Meer informatie over hoe toorun Python code in de U-SQL-Scripts
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Zelfstudie: Aan de slag met het uitbreiden van U-SQL met behulp van Python

Python-uitbreidingen voor de U-SQL kunt ontwikkelaars tooperform massively parallelle uitvoering van Python-code. Hallo volgende voorbeeld illustreert Hallo eenvoudige stappen:

* Gebruik Hallo `REFERENCE ASSEMBLY` instructie tooenable Python-extensies voor Hallo U-SQL-Script
* Met behulp van Hallo `REDUCE` bewerking toopartition Hallo invoergegevens voor een sleutel
* Hallo Python-uitbreidingen voor de U-SQL bevatten een ingebouwde reducer (`Extension.Python.Reducer`) die op elke hoekpunt toegewezen toohello reducer Python-code wordt uitgevoerd
* Hallo U-SQL-script bevat Hallo ingesloten Python-code die een functie die wordt aangeroepen `usqlml_main` die een pandas DataFrame als invoer accepteert en retourneert een pandas DataFrame als uitvoer.

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Hoe Python integreert met U-SQL

### <a name="datatypes"></a>Gegevenstypen

* Zo worden geconverteerd als tekenreeks en numerieke kolommen uit de U-SQL-tussen Pandas en U-SQL
* U-SQL null-waarden zijn geconverteerde tooand van Pandas `NA` waarden

### <a name="schemas"></a>Schema 's

* Index aanvalsvectoren in Pandas worden niet ondersteund in de U-SQL. Alle ingevoerde gegevensframes in Hallo Python functie hebben altijd een 64-bits numerieke index 0 tot en met Hallo aantal rijen min 1. 
* U-SQL-gegevenssets kan geen dubbele kolomnamen hebben
* U-SQL gegevenssets kolomnamen die geen tekenreeksen. 

### <a name="python-versions"></a>Python-versies
Alleen Python 3.5.1 (gecompileerd voor Windows) wordt ondersteund. 

### <a name="standard-python-modules"></a>Standaard Python-modules
Alle Hallo standaard Python-modules zijn opgenomen.

### <a name="additional-python-modules"></a>Extra Python-modules
Afgezien van Python standaardbibliotheken hello, is enkele veelgebruikte python-bibliotheken zijn opgenomen:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Uitzondering berichten
Op dit moment is een uitzondering in Python-code wordt weergegeven als algemene hoekpunt mislukt. In toekomstige hello weergegeven Hallo U-SQL-taak foutberichten Hallo Python uitzonderingsbericht.

### <a name="input-and-output-size-limitations"></a>Invoer en uitvoer groottebeperkingen
Elke hoekpunt heeft een beperkte hoeveelheid geheugen die tooit is toegewezen. Deze limiet is momenteel 6 GB voor een AU. Omdat hello invoer en uitvoer DataFrames moet bestaan in het geheugen van Hallo Python-code, kan niet Hallo totale voor Hallo invoer en uitvoer groter zijn dan 6 GB.

## <a name="see-also"></a>Zie ook
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [U-SQL-scripts ontwikkelen met Data Lake-hulpmiddelen voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [U-SQL-vensterfuncties gebruiken voor Azure Data Lake Analytics-taken](data-lake-analytics-use-window-functions.md)

