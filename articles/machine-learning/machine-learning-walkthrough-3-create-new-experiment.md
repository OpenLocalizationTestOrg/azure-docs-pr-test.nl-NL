---
title: 'Stap 3: Maak een nieuwe Machine Learning-experiment | Microsoft Docs'
description: 'Stap 3 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: een nieuw trainingsexperiment maken in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Kennismaken, stap 3: Een nieuw Azure Machine Learning-experiment maken
Dit is de derde stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Een Machine Learning-werkruimte maken](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)
3. **Een nieuw experiment maken**
4. [Trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Hallo-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md)
6. [Toegang tot Hallo-webservice](machine-learning-walkthrough-6-access-web-service.md)

- - -
Hallo volgende stap in dit scenario is toocreate een experiment in Machine Learning Studio die gebruikmaakt van Hallo gegevensset die wordt geüpload.  

1. Klik in Studio **+ nieuw** onderaan Hallo Hallo-venster.
2. Selecteer **EXPERIMENT**, en selecteer vervolgens 'Leeg Experiment'. 

    ![Een nieuw experiment maken][0]

2. Selecteer Hallo standaard naam Hallo boven aan het papier Hallo experiment en wijzig deze toosomething zinvolle.

    ![Wijzig de naam van experiment][5]
   
   > [!TIP]
   > Het is een goede gewoonte toofill in **samenvatting** en **beschrijving** voor Hallo experiment in Hallo **eigenschappen** deelvenster. Deze eigenschappen kunt u kans toodocument Hallo experiment hello, zodat iedereen die deze later wordt uw doelen en methodologie begrijpen.
   > 
   > ![Experiment eigenschappen][6]
   > 
3. Vouw in het Hallo-module palet toohello links van het experimentcanvas hello **gegevenssets opgeslagen**.
4. Zoeken naar Hallo gegevensset die u hebt gemaakt onder **mijn gegevenssets** en sleep deze naar Hallo canvas. U vindt ook Hallo gegevensset Hallo naam door in te voeren Hallo **Search** vak boven Hallo palet.  

    ![Hallo gegevensset toohello experiment toevoegen][7]

## <a name="prepare-hello-data"></a>Hallo gegevens voorbereiden
U kunt weergeven eerste 100 rijen Hallo gegevens en enkele statische gegevens voor de volledige gegevensset Hallo Hallo: klik op de uitvoerpoort Hallo van Hallo gegevensset (Hallo kleine cirkel Hallo onderin) en selecteer **visualiseren**.  

Omdat het gegevensbestand Hallo niet meegeleverd met kolomkoppen, Studio algemene koppen is opgegeven (Col1, Col2, *enzovoort*). Goede koppen niet essentieel toocreating een model, maar ze eenvoudiger eenvoudiger toowork met Hallo gegevens in Hallo-experiment. Ook wanneer we dit model uiteindelijk in een webservice publiceren, Hallo koppen te identificeren Hallo kolommen toohello gebruiker van Hallo-service.  

We kunt toevoegen met behulp van Hallo kolomkoppen [metagegevens bewerken] [ edit-metadata] module.
Gebruik van Hallo [metagegevens bewerken] [ edit-metadata] module toochange metagegevens gekoppeld aan een dataset. In dit geval we gebruiken deze tooprovide meer beschrijvende namen voor kolomkoppen. 

toouse [metagegevens bewerken][edit-metadata], u eerst een opgeven welke kolommen toomodify (in dit geval ze allemaal.) Geef vervolgens Hallo actie toobe uitgevoerd op deze kolommen (in dit geval kolomkoppen te wijzigen.)

1. Typ in het modulepalet hello, 'metagegevens' in hello **Search** vak. Hallo [metagegevens bewerken] [ edit-metadata] wordt weergegeven in de modulelijst Hallo.

2. Klik en sleep Hallo [metagegevens bewerken] [ edit-metadata] module op Hallo canvas en zet deze neer hieronder Hallo gegevensset we die eerder is toegevoegd.

3. Verbinding maken met de Hallo gegevensset toohello [metagegevens bewerken][edit-metadata]: klikt u op de uitvoerpoort Hallo Hallo gegevensset (Hallo kleine cirkel onderaan Hallo Hallo gegevensset), sleep toohello invoerpoort van [metagegevens bewerken ] [ edit-metadata] (Hallo kleine cirkel Hallo boven aan het Hallo-module), laat u Hallo muisknop los. Hallo gegevensset en module blijven verbonden, zelfs als u ofwel op Hallo canvas verplaatsen.
   
   Hallo-experiment moet nu als volgt uitzien:  
   
   ![Metagegevens bewerken][1]
   
   Hallo rood uitroepteken geeft aan we Hallo-eigenschappen voor deze module nog niet hebt ingesteld. We doen om het dialoogvenster.
   
   > [!TIP]
   > U kunt een opmerking tooa module door te dubbelklikken op Hallo-module en tekstinvoer toevoegen. Hiermee kunt u in één oogopslag zien welke Hallo-module in uw experiment doet. Dubbelklik in dit geval op Hallo [metagegevens bewerken] [ edit-metadata] module en type Hallo Opmerking 'Add kolomkoppen'. Klik ergens anders op Hallo canvas tooclose Hallo-tekstvak. toodisplay Opmerking hello, klikt u op Hallo pijl-omlaag op het Hallo-module.
   > 
   > ![Metagegevens module bewerken met opmerkingen toegevoegd][8]
   > 
4. Selecteer [metagegevens bewerken][edit-metadata], en in Hallo **eigenschappen** deelvenster toohello rechts van het canvas hello, klikt u op **Launch column selector**.

5. In Hallo **kolommen selecteren** dialoogvenster, selecteer alle rijen in Hallo **beschikbare kolommen** en klik op > toomove ze te**geselecteerde kolommen**.
   Hallo dialoogvenster ziet er als volgt:

   ![Kolomkiezer met alle kolommen geselecteerd][2]

6. Klik op Hallo **OK** selectievakje is ingeschakeld.

7. Terug in Hallo **eigenschappen** deelvenster, zoek Hallo **nieuwe kolomnamen** parameter. Geef een lijst met namen voor Hallo 21 kolommen in de gegevensset hello, gescheiden door komma's en in de volgorde van kolommen in dit veld. U kunt Hallo kolommen namen ophalen Hallo gegevensset documentatie op Hallo UCI website of voor het gemak kunt u kopiëren en plakken Hallo lijst na:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   Hallo eigenschappendeelvenster ziet er als volgt:
   
   ![Eigenschappen voor metagegevens bewerken][3]

> [!TIP]
> Als u tooverify Hallo kolomkoppen wilt, Hallo experiment uitvoeren (Klik op **uitvoeren** onder het experimentcanvas Hallo). Wanneer deze is voltooid (Er verschijnt een groen vinkje op [metagegevens bewerken][edit-metadata]), klikt u op de uitvoerpoort Hallo Hallo [metagegevens bewerken] [ edit-metadata] module en selecteer **Visualize**. U kunt Hallo-uitvoer van elke module weergeven in Hallo dezelfde manier tooview Hallo voortgang van Hallo gegevens via Hallo experiment.
> 
> 

## <a name="create-training-and-test-datasets"></a>Training maken en testen van gegevenssets
Sommige gegevens tootrain Hallo-model en sommige tootest moet het.
Dus in de volgende stap Hallo van Hallo experiment, we Hallo gegevensset in twee afzonderlijke gegevenssets splitsen: één voor het trainen van het model en één voor het testen van het.

toodo, gebruiken we Hallo [Split Data] [ split] module.  

1. Hallo zoeken [Split Data] [ split] -module, sleep deze naar Hallo canvas en verbindt u deze toohello [metagegevens bewerken] [ edit-metadata] module.

2. Hallo gesplitste verhouding is standaard 0,5 en Hallo **Randomized gesplitste** parameter is ingesteld. Dit betekent dat een willekeurige helft van Hallo gegevens uitgevoerd via één poort Hallo wordt [Split Data] [ split] -module en de helft via Hallo andere. U kunt deze parameters aanpassen, evenals Hallo **willekeurige seed** parameter toochange Hallo verdeeld over de trainings- en testdoeleinden gegevens. In dit voorbeeld laat we ze-is.
   
   > [!TIP]
   > eigenschap Hallo **fractie van rijen in Hallo eerst uitvoergegevensset** bepaalt hoeveel gegevens Hallo uitvoer via Hallo *links* uitvoerpoort. Bijvoorbeeld als u Hallo verhouding too0.7 instelt, wordt vervolgens 70% van Hallo gegevens uitgevoerd via de poort en 30% links via de juiste poort Hallo Hallo.  
   > 
   > 

3. Dubbelklik op Hallo [Split Data] [ split] module en Hallo opmerking invoeren, ' Training/testen gegevens splitsen 50% '. 

We kunnen Hallo uitvoerwaarden van hello gebruiken [Split Data] [ split] module echter we graag, maar we kiezen toouse Hallo links uitvoer als trainingsgegevens en Hallo rechts als testen uitvoergegevens.  

Zoals vermeld in Hallo [vorige stap](machine-learning-walkthrough-2-upload-data.md), Hallo kosten van een hoge kredietrisico als laag onjuiste vijf keer hoger is dan Hallo kosten van het onjuiste een lage kredietrisico zo hoog. tooaccount voor dit dat er een nieuwe gegevensset die overeenkomt met deze functie kosten gegenereerd. In de nieuwe gegevensset Hallo, elk met een hoog risico voorbeeld vijf keer gerepliceerd terwijl elke laag risico voorbeeld niet is gerepliceerd.   

We kunnen deze replicatie doen met behulp van R-code:  

1. Zoek en sleep Hallo [R-Script uitvoeren] [ execute-r-script] module naar het experimentcanvas Hallo. 

2. Hallo links uitvoerpoort Hallo verbinding [Split Data] [ split] poort ('Dataset1') module toohello eerste invoer Hallo [R-Script uitvoeren] [ execute-r-script] module.

3. Dubbelklik op Hallo [R-Script uitvoeren] [ execute-r-script] module en Voer Hallo-Opmerking 'Instellen kosten aanpassing'.

4. In Hallo **eigenschappen** deelvenster verwijderen Hallo standaardtekst in Hallo **R-Script** parameter en voer dit script:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R-script module Hallo R-Script uitvoeren][9]

Deze dezelfde replicatiebewerking voor elke uitvoer Hallo toodo moet [Split Data] [ split] module zodat deze Hallo trainings- en testdoeleinden gegevens hebben dezelfde Hallo kosten aanpassing. Hallo gemakkelijkste manier toodo dit is de Hallo dupliceren [R-Script uitvoeren] [ execute-r-script] module we zojuist hebt gemaakt en dit toohello verbindt ander uitvoer poort Hallo [Split Data] [ split] module.

1. Klik met de rechtermuisknop Hallo [R-Script uitvoeren] [ execute-r-script] module en selecteer **kopie**.

2. Met de rechtermuisknop op het experimentcanvas hello en selecteer **plakken**.

3. Hallo nieuwe module naar positie slepen en sluit vervolgens de juiste uitvoerpoort Hallo Hallo [Split Data] [ split] eerste invoer-poort van dit nieuwe module toohello [R-Script uitvoeren] [ execute-r-script] module. 

4. Klik onder Hallo Hallo canvas op **uitvoeren**. 

> [!TIP]
> Hallo-exemplaar van Hallo R-Script niet uitvoeren-module bevat Hallo dezelfde als de oorspronkelijke module Hallo script. Wanneer u kopieert en plakt een module op Hallo canvas, behoudt Hallo kopiëren alle Hallo-eigenschappen van het oorspronkelijke Hallo.  
> 
> 

Onze experiment ziet nu er ongeveer als volgt:

![Split-module en R scripts toe te voegen][4]

Zie voor meer informatie over het gebruik van R-scripts in uw experimenten [uw experiment uitbreiden met R](machine-learning-extend-your-experiment-with-r.md).

**Volgende stap: [trainen en evalueren Hallo modellen](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
