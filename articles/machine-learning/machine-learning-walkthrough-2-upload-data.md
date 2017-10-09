---
title: 'Stap 2: Gegevens uploaden naar een Machine Learning-experiment | Microsoft Docs'
description: 'Stap 2 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: het uploaden van openbare gegevens opgeslagen in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Kennismaken, stap 2: Bestaande gegevens uploaden naar een Azure Machine Learning-experiment
Dit is de tweede stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Bestaande gegevens uploaden**
3. [Een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)
6. [Toegang tot Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)

- - -
een Voorspellend model voor kredietrisico toodevelop, moeten we gegevens we kunnen tootrain gebruiken en test u Hallo-model. Voor dit scenario gebruiken we Hallo 'UCI Statlog (Duitse tegoed gegevens) Data Set' uit Hallo UC Irvine Machine Learning-opslagplaats. U kunt deze hier vinden:  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://Archive.ICS.uci.edu/ml/DataSets/Statlog+(German+credit+Data)</a>

We gebruiken Hallo-bestand met de naam **german.data**. Downloaden van dit bestand tooyour lokale vaste schijf.  

Hallo **german.data** gegevensset bevat rijen van 20 variabelen voor 1000 afgelopen aanvragers tegoed. Deze 20 variabelen vertegenwoordigen reeks functies van deze dataset hello (Hallo *functie vector*), waarmee u identificatiekenmerken op voor elke aanvrager tegoed. Een extra kolom in elke rij vertegenwoordigt van de aanvrager Hallo berekende kredietrisico, met 700 aanvrager aangeduid als een lage kredietrisico en 300 als een hoog risico.

Hallo UCI website bevat een beschrijving van Hallo kenmerken van de functie-vector Hallo voor deze gegevens. Dit omvat financiële gegevens, kredietgeschiedenis werkstatus en persoonlijke gegevens. Voor iedere aanvrager een binaire classificatie is opgegeven waarmee wordt aangegeven of ze zich een lage of hoge kredietrisico. 

We gebruiken deze gegevens tootrain een predictive analytics-model. Als we bent klaar, moet het model kunnen tooaccept een functie-vector voor een nieuwe persoon en of hij of zij een lage of hoge kredietrisico is voorspellen.  

Hier volgt een interessante twist. Hallo beschrijving van gegevensset Hallo op Hallo UCI website vermeldingen die het kost als we iemands kredietrisico misclassify.
Als u een hoge kredietrisico Hallo model voorspelt voor iemand die daadwerkelijk een lage kredietrisico is, heeft Hallo model een misclassification doorgevoerd.
Maar Hallo omgekeerde misclassification vijf keer duurder toohello financiële instelling is: indien Hallo model voorspelt een lage kredietrisico voor iemand die daadwerkelijk een hoge kredietrisico is.

Ja, willen we tootrain ons model zodat Hallo kosten van dit laatste type misclassification vijf keer hoger is dan onjuiste Hallo andere manier.
Een eenvoudige manier toodo dit wanneer Hallo model bij ons experiment training is door te dupliceren (vijfmaal) die items die iemand met een hoge kredietrisico vertegenwoordigen. Vervolgens als Hallo model ten onrechte iemand als een lage kredietrisico classificeert wanneer ze daadwerkelijk een hoog risico, Hallo model geen die dezelfde misclassification vijf keer één keer voor elke kopie. Hierdoor neemt Hallo kosten van deze fout in Hallo training resultaten.


## <a name="convert-hello-dataset-format"></a>Hallo gegevensset-indeling converteren
de oorspronkelijke gegevensset Hallo gebruikt een leeg gescheiden-indeling. Machine Learning Studio werkt beter met een bestand met door komma's gescheiden waarden (CSV), zodat we Hallo gegevensset converteren je door spaties vervangen door komma's.  

Er zijn veel manieren tooconvert deze gegevens. Eenzijdige is met behulp van de volgende Windows PowerShell-opdracht Hallo:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Er is een andere manier met behulp van Hallo Unix ype opdracht:  

    sed 's/ /,/g' german.data > german.csv  

In beide gevallen is er een door komma's gescheiden versie Hallo-gegevens in een bestand met de naam gemaakt **german.csv** die we in ons experiment kunt gebruiken.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Hallo gegevensset tooMachine Learning Studio uploaden
Zodra het Hallo-gegevens zijn geconverteerde tooCSV indeling, moeten we tooupload in Machine Learning Studio. 

1. Open Hallo Machine Learning Studio-startpagina ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Klik op Hallo menu ![Menu][1] in Hallo linkerbovenhoek van Hallo-venster, klikt u op **Azure Machine Learning**, selecteer **Studio**, en meld u aan.

3. Klik op **+ nieuw** onderaan Hallo Hallo-venster.

4. Selecteer **GEGEVENSSET**.

5. Selecteer **vanuit het lokale bestand**.

    ![Voeg een gegevensset toe vanuit het lokale bestand][2]

6. In Hallo **uploaden van een nieuwe gegevensset** dialoogvenster, klikt u op **Bladeren** en Hallo zoeken **german.csv** dat u hebt gemaakt.

7. Voer een naam voor de Hallo gegevensset. Voor dit scenario moet aanroepen 'UCI Duits creditcardgegevens'.

8. Selecteer voor gegevenstype **generieke CSV-bestand met geen koptekst (. nh.csv)**.

9. Een beschrijving toevoegen als u wilt.

10. Klik op Hallo **OK** selectievakje is ingeschakeld.  

    ![Hallo gegevensset uploaden][3]

Dit uploadt Hallo gegevens naar een gegevensset-module die u in een experiment gebruiken kunt.

U kunt beheren die u hebt geüpload, tooStudio door te klikken op Hallo gegevenssets **GEGEVENSSETS** tabblad toohello links van de Hallo Studio-venster.

![Gegevenssets beheren][4]

Zie voor meer informatie over het importeren van andere typen gegevens in een experiment [uw trainingsgegevens importeren in Azure Machine Learning Studio](machine-learning-data-science-import-data.md).

**Volgende stap: [een nieuw experiment maken](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
