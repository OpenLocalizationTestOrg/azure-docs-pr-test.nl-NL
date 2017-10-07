---
title: aaaImport gegevens naar Machine Learning Studio | Microsoft Docs
description: Hoe tooimport uw gegevens in Azure Machine Learning Studio van verschillende gegevensbronnen. Meer informatie over welke gegevenstypen en gegevensopmaak worden ondersteund.
keywords: gegevens, gegevensindeling, gegevenstypen, gegevensbronnen, trainingsgegevens importeren
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Uw trainingsgegevens vanuit verschillende gegevensbronnen importeren in Azure Machine Learning Studio
toouse uw eigen gegevens in Machine Learning Studio toodevelop en de trein een predictive analytics-oplossing, kunt u: 

* uploaden van gegevens uit een **lokaal bestand** voor tijd van de vaste schijf toocreate een gegevensset module in uw werkruimte
* toegang tot gegevens uit een van de **online gegevensbronnen** terwijl uw experiment wordt uitgevoerd met behulp van Hallo [importgegevens] [ import-data] module 
* gegevens uit een andere Azure Machine learning **experimenteren** opgeslagen als een gegevensset
* gegevens uit een on-premises **SQL Server-database**

Elk van deze opties wordt beschreven in een van de onderwerpen Hallo Hallo menu hieronder. Deze onderwerpen bevatten informatie over hoe tooimport van deze gegevens verschillende gegevensbronnen toouse in Machine Learning Studio. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Er zijn een aantal voorbeeldgegevenssets beschikbaar in Machine Learning Studio die u voor trainingsgegevens gebruiken kunt. Zie voor meer informatie over deze [hello voorbeeldgegevenssets in Azure Machine Learning Studio gebruiken](machine-learning-use-sample-datasets.md)).
> 
> 

Dit inleidende onderwerp wordt beschreven hoe tooget gegevens gereed voor gebruik in Machine Learning Studio ook en wordt beschreven welke gegevensindelingen en gegevenstypen worden ondersteund. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Gegevens in Azure Machine Learning Studio klaar voor gebruik ophalen
Machine Learning Studio is ontworpen toowork met rechthoekige of tabellaire gegevens, zoals tekstgegevens die gescheiden of gestructureerde gegevens uit een database, maar in sommige gevallen niet-rechthoekige gegevens mogen worden gebruikt.

Het is raadzaam als uw gegevens relatief schoon is. Dat wil zeggen, moet u tootake antwoord problemen zoals zonder aanhalingstekens tekenreeksen voordat u Hallo gegevens naar uw experiment uploaden.

Er zijn echter modules in Machine Learning Studio waarmee manipuleren van gegevens binnen uw experiment beschikbaar. Afhankelijk van Hallo machine learning-algoritmen u wilt gebruiken, moet u mogelijk toodecide hoe u gegevens structurele problemen zoals ontbrekende waarden en sparse gegevens wordt verwerkt en er modules die u bij die helpen kunnen. Zoeken in Hallo **Data Transformation** sectie van het modulepalet Hallo voor modules die deze functies worden uitgevoerd.

U kunt op elk gewenst moment in uw experiment weergeven of downloaden Hallo-gegevens die wordt geproduceerd door een module door te klikken op de uitvoerpoort Hallo. Afhankelijk van de module hello, kunnen er verschillende Downloadinstellingen beschikbaar of hebt u mogelijk kunnen toovisualize Hallo gegevens in uw webbrowser in Machine Learning Studio.

## <a name="data-formats-and-data-types-supported"></a>Opmaak en gegevenstypen worden ondersteund
U kunt een aantal gegevenstypen in uw experiment importeren, afhankelijk van welke mechanisme u tooimport gegevens en waar deze vandaan gebruiken:

* Tekstbestand (.txt)
* Door komma's gescheiden waarden (CSV met een koptekst (.csv) of zonder) (. nh.csv)
* Door tabs gescheiden waarden (TSV met een koptekst (.tsv) of zonder) (. nh.tsv)
* Excel-bestand
* Azure-tabel
* Hive-tabel
* SQL-databasetabel
* OData-waarden
* SVMLight gegevens (.svmlight) (Zie Hallo [SVMLight definitie](http://svmlight.joachims.org/) voor indeling informatie)
* Kenmerk Relation File Format (ARFF) gegevens (.arff) (Zie Hallo [ARFF definitie](http://weka.wikispaces.com/ARFF) voor indeling informatie)
* ZIP-bestand (.zip)
* R-object of de werkruimte-bestand (. RData)

Als u gegevens in een indeling zoals ARFF met metagegevens importeert, wordt in Machine Learning Studio deze metagegevens toodefine Hallo kop en het gegevenstype van elke kolom gebruikt.

Als u gegevens zoals TSV- of CSV-indeling waarin deze metagegevens niet importeert, gegevenstype Machine Learning Studio Hallo voor elke kolom van steekproeven Hallo-gegevens. Als Hallo gegevens ook geen kolomkoppen, biedt Machine Learning Studio standaardnamen.

U kunt expliciet opgeven of Hallo koppen en gegevenstypen voor kolommen met Hallo wijzigen [metagegevens bewerken][edit-metadata].

Hallo volgende **gegevenstypen** worden herkend door Machine Learning Studio:

* Tekenreeks
* Geheel getal
* dubbele
* Booleaanse waarde
* Datum/tijd
* TimeSpan

Machine Learning Studio maakt gebruik van een interne gegevenstype aangeroepen ***gegevenstabel*** toopass gegevens tussen modules. U kunt uw gegevens expliciet converteren naar gegevens tabelindeling Hallo met [converteren tooDataset] [ convert-to-dataset] module.

Elke module die indelingen dan gegevenstabel accepteert geconverteerd Hallo gegevens tooData tabel achtergrond voordat deze de volgende module toohello wordt doorgegeven.

U kunt indien nodig, gegevenstabel naar CSV, TSV, ARFF, of SVMLight notatie met andere modules conversie converteren.
Zoeken in Hallo **gegevens indeling conversies** sectie van het modulepalet Hallo voor modules die deze functies worden uitgevoerd.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
