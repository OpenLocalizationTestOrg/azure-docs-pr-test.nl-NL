---
title: aaaA eenvoudig experiment in Machine Learning Studio | Microsoft Docs
description: Deze zelfstudie over Machine Learning leidt u door een eenvoudig gegevenswetenschapexperiment. We moet Hallo prijs van een auto met een regression-algoritme voorspellen.
keywords: experiment,lineaire regressie,machine learning-algoritmen,zelfstudie over machine learning,voorspellende modelleringstechnieken,gegevenswetenschapexperiment
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Zelfstudie over Machine Learning: uw eerste gegevenswetenschapexperiment maken in Azure Machine Learning Studio

Als u **Azure Machine Learning Studio** niet eerder hebt gebruikt, biedt deze zelfstudie een goede basis.

In deze zelfstudie behandelen we hoe toouse Studio voor Hallo dit de eerste keer toocreate een machine learning-experiment. Hallo-experiment wordt een analytische model dat Hallo prijs van een auto op basis van verschillende variabelen, zoals het merk en technische specificaties voorspelt testen.

> [!NOTE]
> Deze zelfstudie leert u Hallo basisprincipes van hoe toodrag-en-neerzetten modules naar uw experiment ze met elkaar verbinden, Hallo experiment uitvoeren en bekijkt hello resultaten. We zullen niet toodiscuss Hallo algemeen onderwerp van machine learning of hoe Hallo 100 + ingebouwde algoritmen en gegevens manipulatie modules opgenomen in Studio tooselect en het gebruik.
>
>Als u nieuwe toomachine learning, Hallo video series [Gegevenswetenschap voor beginnende gebruikers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) mogelijk een goede plaats toostart. Deze video-serie is een uitstekende inleiding toomachine learning met alledaagse taal en -concepten.
>
>Als u bekend met machine learning bent, maar u meer algemene informatie over Machine Learning Studio en Hallo machine learning-algoritmen die deze bevat zoekt, zijn er goede bronnen:
>
- [Wat is Machine Learning Studio?](machine-learning-what-is-ml-studio.md) - Dit geeft een overzicht van Studio.
- [Machine learning-algoritme voorbeelden voor alledaagse](machine-learning-basics-infographic-with-algorithm-examples.md) -deze infographic is handig als u meer informatie over de verschillende soorten machine learning-algoritmen opgenomen in Machine Learning Studio Hallo toolearn wilt.
- [Machine Learning-handleiding](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -in deze gids vindt soortgelijke informatie als Hallo infographic hierboven, maar in een interactieve indeling.
- [Machine learning-algoritme-referentieoverzicht](machine-learning-algorithm-cheat-sheet.md) en [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) -deze Downloadbare poster en de bijbehorende artikel Hallo Studio algoritmen in de diepte bespreken.
- [Machine Learning Studio: Algoritme en Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) -dit is de volledige verwijzing Hallo voor alle Studio-modules, waaronder machine learning-algoritmen

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Op welke wijze is Machine Learning Studio nuttig?

Machine Learning Studio maakt het eenvoudig tooset van een experiment met behulp van slepen en neerzetten modules voorgeprogrammeerde met voorspellende modelleringstechnieken.

In de interactieve, visuele werkruimte sleept u ***gegevenssets*** en analyse***modules*** naar een interactief canvas. U ze samen tooform verbindt een ***experimenteren*** die u uitvoert in Machine Learning Studio.
U ***een model maken***, ***Hallo model trainen***, en ***score en test Hallo model***.

U kunt bladeren het modelontwerp Hallo experiment bewerken en biedt uitgevoerd totdat het Hallo resultaten die u zoekt. Wanneer uw model klaar is, kunt u het publiceren als een ***webservice***, zodat anderen voorspellingen kunnen krijgen voor de nieuwe gegevens die zij toesturen.

## <a name="open-machine-learning-studio"></a>Machine Learning Studio openen

tooget gestart met Studio, ga te[https://studio.azureml.net](https://studio.azureml.net). Als u zich eerder hebt aangemeld bij Machine Learning Studio, klikt u op **Sign in**. Klik anders op **Sign Up** en kies tussen gratis en betaalde opties.

![Meld u aan tooMachine Learning Studio][sign-in-to-studio]
<br/>
***Meld u aan tooMachine Learning Studio***

## <a name="five-steps-toocreate-an-experiment"></a>Toocreate vijf stappen een experiment

In deze machine learning-zelfstudie past u vijf eenvoudige stappen toobuild een experiment in Machine Learning Studio toocreate, trein, volgen en het model beoordelen:

- **Een model maken**
    - [Stap 1: gegevens ophalen]
    - [Stap 2: Hallo gegevens voorbereiden]
    - [Stap 3: functies definiëren]
- **Hallo-model trainen**
    - [Stap 4: een leeralgoritme kiezen en toepassen]
- **Score en test Hallo model**
    - [Stap 5: prijzen van nieuwe auto's voorspellen]

[Stap 1: gegevens ophalen]: #step-1-get-data
[Stap 2: Hallo gegevens voorbereiden]: #step-2-prepare-the-data
[Stap 3: functies definiëren]: #step-3-define-features
[Stap 4: een leeralgoritme kiezen en toepassen]: #step-4-choose-and-apply-a-learning-algorithm
[Stap 5: prijzen van nieuwe auto's voorspellen]: #step-5-predict-new-automobile-prices

> [!TIP] 
> U vindt een werkexemplaar Hallo volgende experiment in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Ga te**[uw eerste gegevenswetenschap experimenteren - prijzen auto's voorspellen](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  en klik op **openen in Studio** toodownload een kopie van het Hallo-experiment in uw Machine Learning Studio-werkruimte.


## <a name="step-1-get-data"></a>Stap 1: gegevens ophalen

Hallo eerste wat u moet tooperform machine learning is gegevens.
Machine Learning Studio bevat een aantal voorbeeldgegevenssets die u kunt gebruiken. Daarnaast kunt u uit tal van bronnen gegevens importeren. In dit voorbeeld gebruiken we Hallo voorbeeldgegevensset **Automobile price data (Raw)**, die opgenomen in de werkruimte.
Deze gegevensset bevat vermeldingen voor verschillende auto's, inclusief informatie over het merk, het model, de technische specificaties en de prijs.

Hier ziet u hoe tooget gegevensset Hallo in uw experiment.

1. Een nieuw experiment maken door te klikken op **+ nieuw** aan de onderkant van de Hallo van Hallo Machine Learning Studio-venster, selecteer **EXPERIMENTEREN**, en selecteer vervolgens **leeg Experiment**.

2. Hallo-experiment krijgt een standaardnaam die u Hallo boven aan het Hallo-canvas zien kunt. Deze tekst selecteren en de naam toosomething zinvolle, bijvoorbeeld **prijzen auto's voorspellen**. Hallo-naam moet niet toobe uniek zijn.

    ![Wijzig de naam van Hallo experiment][rename-experiment]

2. toohello links van het experimentcanvas Hallo zich een palet met gegevenssets en modules. Type **auto** in het zoekvak Hallo Hallo boven aan dit palet toofind Hallo gegevensset met het label **Automobile price data (Raw)**. Sleep deze gegevensset toohello-experimentcanvas.

    ![Hallo auto gegevensset zoeken en sleep deze naar het experimentcanvas Hallo][type-automobile]
    <br/>
    ***Hallo auto gegevensset zoeken en sleep deze naar het experimentcanvas Hallo***

toosee wat deze gegeven eruitzien, klikt u op de uitvoerpoort Hallo HALLO hallo auto gegevensset onderaan in en selecteer vervolgens **Visualize**.

![Klik op de uitvoerpoort Hallo en selecteer 'Visualiseren'][select-visualize]
<br/>
***Klik op de uitvoerpoort Hallo en selecteer 'Visualiseren'***

> [!TIP]
> Gegevenssets en modules hebben invoer en uitvoerpoorten dat wordt vertegenwoordigd door cirkeltjes - ingangspoorten boven Hallo uitvoer poorten Hallo onderaan.
een stroom van gegevens door uw experiment toocreate, maakt u verbinding met een uitvoerpoort van één module tooan invoerpoort van een andere.
Op elk gewenst moment kunt u de uitvoerpoort Hallo van een dataset of module toosee welke gegevens Hallo ziet er op dat moment in de gegevensstroom Hallo.

Elk exemplaar van een auto wordt weergegeven als een rij in deze dataset voorbeeld en Hallo variabelen die zijn gekoppeld aan elke auto worden weergegeven als kolommen. Hallo variabelen gegeven voor een specifieke auto, gaan we tootry toopredict Hallo prijs in de meest rechtse kolom (kolom 26, met de titel ' price').

![Hallo auto gegevens weergeven in visualisatievenster Hallo-gegevens][visualize-auto-data]
<br/>
***Hallo auto gegevens weergeven in visualisatievenster Hallo-gegevens***

Sluit Hallo visualisatievenster door te klikken op Hallo '**x**' in de rechterbovenhoek Hallo.

## <a name="step-2-prepare-hello-data"></a>Stap 2: Hallo gegevens voorbereiden

Normaal gesproken moet een gegevensset worden voorverwerkt voordat deze kan worden geanalyseerd. Bijvoorbeeld, u mogelijk opgevallen Hallo waarden aanwezig zijn in Hallo kolommen van verschillende rijen ontbreken. Deze ontbrekende waarden moeten toobe opgeschoond, zodat het Hallo-model correct Hallo gegevens kunt analyseren. In ons geval verwijderen we de rijen met ontbrekende waarden. Bovendien Hallo **normalized-losses** kolom heeft een groot deel van de ontbrekende waarden zo worden uitgesloten die kolom uit Hallo model helemaal.

> [!TIP]
> Reinigingstape Hallo ontbrekende invoergegevens is een vereiste voor het gebruik van de meeste Hallo-modules.

Eerst wordt een module die Hallo verwijdert toevoegen **normalized-losses** kolom volledig, en voeg er een andere module die rijen met ontbrekende gegevens verwijdert.

1. Type **kolommen selecteren** in het zoekvak Hallo Hallo boven aan het Hallo-module palet toofind hello [Select Columns in Dataset] [ select-columns] -module, sleept u deze toohello experimentcanvas . Deze module kunt tooselect welke kolommen met gegevens die we wilt tooinclude in of uitsluiten Hallo model.

2. Verbinding maken met de uitvoerpoort Hallo Hallo **Automobile price data (Raw)** gegevensset toohello invoer poort Hallo [Select Columns in Dataset] [ select-columns] module.

    ![Toevoegen Hallo 'Kolommen in gegevensset selecteren' module toohello-experimentcanvas en koppel][type-select-columns]
    <br/>
    ***Toevoegen Hallo 'Kolommen in gegevensset selecteren' module toohello-experimentcanvas en koppel***

3. Klik op Hallo [Select Columns in Dataset] [ select-columns] module en klikt u op **Launch column selector** in Hallo **eigenschappen** deelvenster.

    - Klik aan de linkerkant Hallo op **met regels**
    - Klik onder **Begin With** op **All columns**. Dit zorgt ervoor dat [Select Columns in Dataset] [ select-columns] toopass via alle Hallo kolommen (met uitzondering van die kolommen we over tooexclude).
    - Selecteer in het Hallo-vervolgkeuzelijsten **uitsluiten** en **kolomnamen**, en klik vervolgens in het tekstvak Hallo. Er wordt een lijst met kolommen weergegeven. Selecteer **normalized-losses**, en het tekstvak toegevoegde toohello is.
    - Klik op Hallo vinkje (OK) knop tooclose Hallo kolomkiezer (op Hallo rechtsonder).

    ![Hallo kolomkiezer Start en Hallo 'normalized-losses' kolom uitsluiten][launch-column-selector]
    <br/>
    ***Hallo kolomkiezer Start en Hallo 'normalized-losses' kolom uitsluiten***

    Nu Hallo eigenschappendeelvenster voor **Select Columns in Dataset** geeft aan dat deze worden doorgegeven alle kolommen uit de dataset Hallo behalve **normalized-losses**.

    ![Hallo eigenschappendeelvenster bevat dat die 'normalized-losses' Hallo-kolom is uitgesloten.][showing-excluded-column]
    <br/>
    ***Hallo eigenschappendeelvenster bevat dat die 'normalized-losses' Hallo-kolom is uitgesloten.***

    > [!TIP]
    U kunt een opmerking tooa module door te dubbelklikken op Hallo-module en tekstinvoer toevoegen. Hiermee kunt u in één oogopslag zien welke Hallo-module in uw experiment doet. Dubbelklik in dit geval op Hallo [Select Columns in Dataset] [ select-columns] module en type Hallo opmerking "Uitsluiten genormaliseerd verliezen."
    >
    >


    ![Dubbelklik op een module tooadd een opmerking][add-comment]
    <br/>
    ***Dubbelklik op een module tooadd een opmerking***

3. Sleep Hallo [Clean Missing Data] [ clean-missing-data] module toohello experimenteren canvas en verbindt u deze toohello [Select Columns in Dataset] [ select-columns] module. In Hallo **eigenschappen** deelvenster **hele rij verwijderen** onder **Cleaning mode**. Dit zorgt ervoor dat [Clean Missing Data] [ clean-missing-data] tooclean Hallo gegevens door het verwijderen van rijen met ontbrekende waarden. Dubbelklik op Hallo-module en typ Hallo-Opmerking 'Rijen met ontbrekende waarde verwijderen'.

    ![Hallo reinigingstape modus te ' hele rij verwijderen' voor Hallo 'Clean Missing Data' module][set-remove-entire-row]
    <br/>
    ***Hallo reinigingstape modus te ' hele rij verwijderen' voor Hallo 'Clean Missing Data' module***

4. Hallo-experiment uitvoeren door te klikken op **uitvoeren** Hallo Hallo pagina onderaan in.

    Wanneer Hallo experiment is voltooid, hebben alle Hallo modules een groen vinkje tooindicate die deze zijn voltooid. U ziet ook Hallo **uitgevoerd** status in de rechterbovenhoek Hallo.

![Na het uitvoeren van het ziet Hallo-experiment er ongeveer als volgt][early-experiment-run]
<br/>
***Na het uitvoeren van het ziet Hallo-experiment er ongeveer als volgt***

> [!TIP]
> Waarom we Hallo experiment nu uitvoeren? Door actieve Hallo-experiment Hallo kolomdefinities voor onze gegevens uit de dataset hello, via Hallo doorgeven [Select Columns in Dataset] [ select-columns] -module, en via Hallo [Clean Missing Data] [ clean-missing-data] module. Dit betekent dat alle modules die we verbinding te maken[Clean Missing Data] [ clean-missing-data] heeft ook dezelfde informatie.

Hallo-experiment toothis punt hebben we schone Hallo gegevens is. Als u wilt dat tooview Hallo gereinigd gegevensset, klikt u op Hallo uitvoerpoort Hallo links [Clean Missing Data] [ clean-missing-data] module en selecteer **Visualize**. U ziet dat Hallo **normalized-losses** kolom is niet meer opgenomen en er zijn geen ontbrekende waarden.

Nu dat Hallo gegevens opgeschoond zijn, we klaar toospecify welke functies we gaan toouse in Hallo Voorspellend model.

## <a name="step-3-define-features"></a>Stap 3: functies definiëren

In machine learning zijn *functies* afzonderlijke meetbare eigenschappen van iets waarin u geïnteresseerd bent. In onze gegevensset staat elke rij voor één auto en elke kolom bevat een kenmerk van die auto.

Zoeken naar een goede set kenmerken voor het maken van een Voorspellend model moet u experimenteren en kennis over Hallo probleem u toosolve. Sommige functies zijn beter voor het voorspellen van Hallo doel dan andere. Bovendien bestaat er tussen sommige kenmerken een nauwe correlatie. Deze kunnen daarom worden verwijderd. Bijvoorbeeld, zijn city-mpg en highway-mpg nauw verwant zodat we kunt een houden en andere Hallo verwijderen zonder aanzienlijke gevolgen hebben voor de voorspelling Hallo.

Laten we een model bouwen dat gebruikmaakt van een subset van Hallo functies in onze gegevensset. U kunt later terugkeren en andere kenmerken selecteren, Hallo experiment opnieuw uitvoeren en zien als u betere resultaten krijgt. Maar toostart, gaan we proberen Hallo volgende kenmerken:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Sleep nog een [Select Columns in Dataset] [ select-columns] module toohello experimenteren canvas. Hallo links uitvoerpoort Hallo verbinding [Clean Missing Data] [ clean-missing-data] module-invoer toohello Hallo [Select Columns in Dataset] [ select-columns] module.

    ![Verbinding maken met de Hallo 'Kolommen in gegevensset selecteren' module toohello 'Clean Missing Data' module][connect-clean-to-select]
    <br/>
    ***Verbinding maken met de Hallo 'Kolommen in gegevensset selecteren' module toohello 'Clean Missing Data' module***

2. Dubbelklik op Hallo-module en typ "Select functies voor de prognose."

2. Klik op **Launch column selector** in Hallo **eigenschappen** deelvenster.

3. Klik op **With rules**.

4. Klik onder **Begin With** op **No columns**. Selecteer in de filterrij hello, **opnemen** en **kolomnamen** en onze lijst met kolomnamen in het tekstvak Hallo selecteert. Dit stuurt Hallo module toonot pass through-kolommen (functies), behalve Hallo toepassingsgroepen die wij opgeven.

5. Klik op Hallo vinkje (OK).

    ![Hallo kolommen (functies) tooinclude in Hallo voorspelling selecteren][select-columns-to-include]
    <br/>
    ***Hallo kolommen (functies) tooinclude in Hallo voorspelling selecteren***

Dit resulteert in een gefilterde gegevensset met alleen Hallo functies willen we toopass toohello learning-algoritme we in de volgende stap Hallo gebruiken. U kunt later terugkeren en het opnieuw proberen met een andere selectie kenmerken.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Stap 4: een leeralgoritme kiezen en toepassen

Nu dat Hallo gegevens klaar is, bestaat een Voorspellend model bouwen uit trainen en te testen. We gebruiken onze gegevens tootrain Hallo-model en controleert we Hallo model toosee hoe nauwkeurig is kunnen toopredict prijzen.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*Classificatie* en *regressie* zijn twee soorten beheerde machine learning-algoritmen. Classificatie voorspelt een antwoord uit een gedefinieerde set categorieën, zoals een kleur (rood, blauw of groen). Regressie is gebruikte toopredict een getal.

Aangezien we prijs toopredict, dat een getal is, gebruiken we een regression-algoritme. In dit voorbeeld gebruiken we een eenvoudig *lineair regressiemodel*.

> [!TIP]
> Als u meer informatie over de verschillende soorten machine learning-algoritmen toolearn wilt en wanneer toouse ze u mogelijk Hallo eerste video bekijken in Hallo Gegevenswetenschap voor beginnende gebruikers reeks, [Hallo vijf gegevens wetenschappelijke antwoorden op vragen](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). U kunt ook zoeken op Hallo infographic [Machine learning-algoritme voorbeelden voor alledaagse](machine-learning-basics-infographic-with-algorithm-examples.md), of uitchecken Hallo [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).

We trainen Hallo model door middel van een set gegevens die Hallo prijs bevat. Hallo model scant Hallo gegevens en zoeken naar correlatie tussen een auto-functies en de prijs. Klik er Hallo model wordt getest - we een aantal functies voor auto's, die we bekend met bent geven en Zie hoe dicht in Hallo model toopredicting Hallo bekende prijs wordt geleverd.

We gebruiken onze gegevens voor zowel Hallo model trainings- en testen van het door het Hallo-gegevens verdelen in afzonderlijke trainings- en testdoeleinden gegevenssets.

1. Selecteer en sleep Hallo [Split Data] [ split] module toohello experimenteren canvas en verbindt dit laatste toohello [Select Columns in Dataset] [ select-columns] module.

2. Klik op Hallo [Split Data] [ split] module tooselect deze. Hallo zoeken **fractie van rijen in Hallo eerst uitvoergegevensset** (in Hallo **eigenschappen** deelvenster toohello rechts van het canvas Hallo) en stel deze too0.75. Deze manier kunnen we 75 procent van de tootrain Hallo-Hallo gegevensmodel gebruiken en 25 procent voor het testen van hinderen (later kunt u experimenteren met het gebruik van verschillende percentages).

    ![Set Hallo fractie van Hallo 'Split Data' module too0.75 splitsen][set-split-data-percentage]
    <br/>
    ***Set Hallo fractie van Hallo 'Split Data' module too0.75 splitsen***

    > [!TIP]
    > Door het wijzigen van Hallo **willekeurige seed** parameter, kunt u verschillende willekeurig samples voor trainings- en testdoeleinden produceren. Deze parameter bepaalt Hallo seeding van de pseudo-willekeurige nummergenerator Hallo.

2. Hallo-experiment uitvoeren. Wanneer Hallo experiment wordt uitgevoerd, Hallo [Select Columns in Dataset] [ select-columns] en [Split Data] [ split] modules kolom definities toohello doorgeven modules die we hierna zullen toevoegen.  

3. tooselect hello learning-algoritme, vouw Hallo **Machine Learning** categorie in Hallo module palet toohello links Hallo canvas uit en vouw vervolgens **Model initialiseren**. Hiermee worden verschillende categorieën die gebruikte tooinitialize machine learning-algoritmen kunnen worden weergegeven. Selecteer voor dit experiment Hallo [lineaire regressie] [ linear-regression] module onder Hallo **regressie** categorie en sleep het experimentcanvas toohello.
(U kunt ook de module Hallo vinden door 'linear regression' hello palet zoekvak te typen.)

4. Zoek en sleep Hallo [Train Model] [ train-model] module toohello experimenteren canvas. Verbinding maken met uitvoer Hallo Hallo [lineaire regressie] [ linear-regression] module toohello links invoer Hallo [Train Model] [ train-model] module en maak verbinding Hallo training gegevensuitvoer (poort links) Hallo [Split Data] [ split] module toohello juiste invoerwaarden Hallo [Train Model] [ train-model] module.

    ![Verbinding maken met de Hallo 'Train-Model' module tooboth Hallo 'Linear Regression' en 'Split Data'-modules][connect-train-model]
    <br/>
    ***Verbinding maken met de Hallo 'Train-Model' module tooboth Hallo 'Linear Regression' en 'Split Data'-modules***

5. Klik op Hallo [Train Model] [ train-model] -module, klikt u op **Launch column selector** in Hallo **eigenschappen** deelvenster en selecteer vervolgens Hallo **prijs** kolom. Dit is dat het model momenteel toopredict is Hallo-waarde.

    U selecteert Hallo **prijs** kolom in de kolomkiezer Hallo door deze te verplaatsen van Hallo **beschikbare kolommen** lijst toohello **kolommen geselecteerd** lijst.

    ![Hallo prijs kolom voor Hallo 'Train-Model' module selecteren][select-price-column]
    <br/>
    ***Hallo prijs kolom voor Hallo 'Train-Model' module selecteren***

6. Hallo-experiment uitvoeren.

We hebben nu een getraind regressiemodel dat gebruikt tooscore nieuwe auto gegevens toomake prijs voorspellingen worden kan.

![Na uitvoering is ziet Hallo experiment er nu ongeveer het volgende][second-experiment-run]
<br/>
***Na uitvoering is ziet Hallo experiment er nu ongeveer het volgende***

## <a name="step-5-predict-new-automobile-prices"></a>Stap 5: prijzen van nieuwe auto's voorspellen

Nu dat we Hallo-model met 75 procent van onze gegevens hebben getraind, kunnen we deze gebruiken tooscore Hallo overige 25 procent Hallo gegevens toosee hoe goed model werkt.

1. Zoek en sleep Hallo [Score Model] [ score-model] module toohello experimenteren canvas. Verbinding maken met uitvoer Hallo Hallo [Train Model] [ train-model] module toohello invoerpoort van links [Score Model][score-model]. Verbinding maken met de Hallo test gegevensuitvoer (rechterpoort) van Hallo [Split Data] [ split] module toohello rechts invoer-poort van [Score Model][score-model].

    ![Verbinding maken met de Hallo 'Score-Model' module tooboth Hallo 'Train-Model' en 'Split Data'-modules][connect-score-model]
    <br/>
    ***Verbinding maken met de Hallo 'Score-Model' module tooboth Hallo 'Train-Model' en 'Split Data'-modules***

2. Hallo experiment uitvoeren en weergeven van Hallo-uitvoer van Hallo [Score Model] [ score-model] module (Klik op de uitvoerpoort Hallo van [Score Model] [ score-model] en selecteer **Visualiseren**). Hallo uitvoer geeft Hallo voorspelde waarden voor de prijs en bekende waarden uit de testgegevens Hallo Hallo.  

    ![Uitvoer van de module van de 'Score-Model' Hallo][score-model-output]
    <br/>
    ***Uitvoer van de module van de 'Score-Model' Hallo***

3. Ten slotte testen we Hallo kwaliteit van Hallo resultaten. Selecteer en sleep Hallo [Evaluate Model] [ evaluate-model] module toohello canvas experimenteren en uitvoer Hallo Hallo verbinding [Score Model] [ score-model] module toohello links van de invoer van [Evaluate Model][evaluate-model].

    > [!TIP]
    > Er zijn twee invoerpoorten op Hallo [Evaluate Model] [ evaluate-model] module omdat het gebruikte toocompare twee modellen naast elkaar kan zijn. Later kunt u een ander algoritme toohello experiment toevoegen en gebruiken [Evaluate Model] [ evaluate-model] toosee waarvoor een betere resultaten oplevert.

4. Hallo-experiment uitvoeren.

tooview hello uitvoer van Hallo [Evaluate Model] [ evaluate-model] -module, klikt u op de uitvoerpoort Hallo en selecteer vervolgens **Visualize**.

![Evaluatieresultaten voor Hallo experiment][evaluation-results]
<br/>
***Evaluatieresultaten voor Hallo experiment***

Hallo volgende statistieken worden weergegeven voor het model:

- **Mean Absolute Error** (MAE): gemiddelde aan absolute fouten Hallo (een *fout* Hallo verschil is tussen Hallo voorspelde waarde en de werkelijke waarde Hallo).
- **Root Mean Squared Error** (RMSE): Hallo vierkantswortel van Hallo gemiddelde aan gekwadrateerde fouten voor de voorspellingen op Hallo testgegevensset.
- **Relative Absolute Error**: Hallo gemiddelde aan absolute fouten relatieve toohello absolute verschil tussen de werkelijke waarden en Hallo gemiddelde van alle werkelijke waarden.
- **Relative Squared Error**: Hallo gemiddelde aan gekwadrateerde fouten relatieve toohello kwadraat verschil tussen de werkelijke waarden Hallo en Hallo gemiddelde van alle werkelijke waarden.
- **Determinatiecoëfficiënt**: ook wel bekend als Hallo **r²-waarde**, dit is een statistische meetwaarde die aangeeft hoe goed een model Hallo gegevens past.

Voor elk van de fout Hallo is statistieken, kleinere beter. Een kleinere waarde geeft aan dat Hallo voorspellingen meer overeenkomt met de werkelijke waarden Hallo. Voor **determinatiecoëfficiënt**, hello dichter bij de waarde ervan tooone (1.0) Hallo betere Hallo voorspellingen.

## <a name="final-experiment"></a>Laatste experiment

Hallo laatste experiment ziet er ongeveer als volgt:

![Hallo laatste experiment][complete-linear-regression-experiment]
<br/>
***Hallo laatste experiment***

## <a name="next-steps"></a>Volgende stappen

Nu dat u Hallo eerste machine learning-zelfstudie hebt voltooid en uw experiment instellen hebt, kunt u doorgaan tooimprove Hallo model en vervolgens implementeren als webservice voorspeld.

- **Herhalen tootry tooimprove Hallo model** -u kunt bijvoorbeeld Hallo-functies die u uw voorspelling gebruikt wijzigen. Of u kunt de eigenschappen Hallo Hallo wijzigen [lineaire regressie] [ linear-regression] algoritme of probeer een ander algoritme kan worden overgeslagen. Kunt u zelfs meerdere machine learning-algoritmen tooyour experiment in één keer toevoegen en twee van deze te vergelijken met behulp van Hallo [Evaluate Model] [ evaluate-model] module.
Voor een voorbeeld van hoe toocompare meerdere modellen in een enkel experiment zien [vergelijken Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy elke herhaling van uw experiment, gebruik Hallo **SAVE AS** knop Hallo onder Hallo pagina aan. U kunt alle Hallo herhalingen van uw experiment weergeven door te klikken op **weergave uitvoeren geschiedenis** Hallo Hallo pagina onderaan in. Zie [Iteraties van experimenten beheren in Azure Machine Learning Studio][runhistory] voor meer informatie.

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Hallo model als een Voorspellend webservice implementeren** : wanneer u tevreden met het model bent, kunt u dit implementeren als een web service toobe toopredict prijzen van auto gebruikt met behulp van nieuwe gegevens. Zie [Een Azure Machine Learning-webservice implementeren][publish] voor meer informatie.

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Wilt u meer toolearn? Zie voor een uitgebreid en gedetailleerd overzicht van Hallo-proces voor het maken, training, scores en implementeren van een model [een voorspellende oplossing ontwikkelen met behulp van Azure Machine Learning][walkthrough].

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
