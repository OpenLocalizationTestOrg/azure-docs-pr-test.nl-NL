---
title: zelfstudie voor R-taal voor Machine Learning aaaQuickstart | Microsoft Docs
description: Deze zelfstudie tooget gestart snel Hallo R taal gebruiken met Azure Machine Learning Studio toocreate een prognosemodel oplossing programming R gebruiken.
keywords: Quick Start, r-taal, de programmeertaal r, programming r-zelfstudie
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Quick Start-zelfstudie voor Hallo R programmeertaal voor Azure Machine Learning

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Inleiding
Deze zelfstudie snel aan de slag kunt u snel starten Azure Machine Learning met behulp van de programmeertaal Hallo R uitbreiden. Volg deze zelfstudie toocreate programming R, testen en R-code in Azure Machine Learning uitvoeren. Als u de zelfstudie doorloopt, maakt u een volledige prognoses oplossing met behulp van Hallo R taal in Azure Machine Learning.  

Microsoft Azure Machine Learning bevat veel krachtige machine learning en manipulatie modules. Hallo krachtige R taal heeft als Hallo lingua franca van analytics zijn beschreven. Manipulatie analytics en gegevens in Azure Machine Learning kan worden uitgebreid met R. Deze combinatie biedt Hallo schaalbaarheid en het gemak van de implementatie van Azure Machine Learning met Hallo flexibiliteit en grondige analyse van R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Prognose en Hallo gegevensset
Prognose is veel werknemers en wel handig analytische methode. Algemeen gebruik bereik van het voorspellen van de verkoop van seizoensgebonden items, optimaal voorraadbeheer, toopredicting macro-economische variabelen te bepalen. Prognose gewoonlijk wordt uitgevoerd met time series-modellen.

Reeks tijdgegevens zijn gegevens waarin Hallo waarden een tijdsindex hebben. Hallo tijdsindex worden regelmatig, bijvoorbeeld elke maand of elke minuut of onregelmatig. Een tijdreeksmodel is gebaseerd op een reeksgegevens. Hallo R programmeertaal bevat een flexibele framework en de uitgebreide analytics voor tijd reeksgegevens.

In deze snelstartgids wordt worden werken met Californië zuivelproductie en prijzen van gegevens. Deze gegevens omvatten maandelijkse informatie op Hallo productie van verschillende producten en Hallo prijs van melkvet, een benchmark basisproduct.

Hallo-gegevens in dit artikel, samen met het R-scripts gebruikt kunnen worden [hier gedownload][download]. Deze gegevens is oorspronkelijk gemaakt van gegevens van Hallo universiteit van Wisconsin op http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>Organisatie
We zullen verschillende stappen doorlopen terwijl u leert hoe toocreate, testen en analytics en data manipulatie R-code in hello Azure Machine Learning-omgeving uitvoeren.  

* Eerst verkennen we Hallo grondbeginselen van het gebruik van Hallo R taal in hello Azure Machine Learning Studio-omgeving.
* Vervolgens wordt de voortgang toodiscussing verschillende aspecten van i/o voor gegevens, R-code en afbeeldingen in hello Azure Machine Learning-omgeving.
* We wordt vervolgens Hallo eerste deel van onze prognoses oplossing maken door het maken van code voor het reinigen van gegevens en transformatie.
* Met onze gegevens voorbereid wordt uitgevoerd, er een analyse van Hallo correlatie tussen verschillende Hallo variabelen in onze gegevensset.
* We gaan ten slotte een seizoen prognoses tijdreeksmodel voor maken.

## <a id="mlstudio"></a>Interactie met R-taal in Machine Learning Studio
Deze sectie leert u enkele van de basisprincipes van de interactie met de programmeertaal Hallo R in Hallo Machine Learning Studio-omgeving. Hallo R taal biedt een krachtig hulpprogramma toocreate aangepast analytics en data manipulatie modules binnen hello Azure Machine Learning-omgeving.

Ik gebruik RStudio toodevelop, testen en foutopsporing R-code op kleine schaal. Deze code wordt vervolgens knippen en plakken in een [R-Script uitvoeren] [ execute-r-script] -module in Machine Learning Studio gereed toorun.  

### <a name="hello-execute-r-script-module"></a>Hallo-module voor R-Script uitvoeren
In Machine Learning Studio R scripts worden uitgevoerd binnen Hallo [R-Script uitvoeren] [ execute-r-script] module. Een voorbeeld van Hallo [R-Script uitvoeren] [ execute-r-script] module in Machine Learning Studio wordt weergegeven in afbeelding 1.

 ![R programmeertaal: Hallo R-Script niet uitvoeren-module is geselecteerd in Machine Learning Studio][1]

*Afbeelding 1. Hallo Machine Learning Studio-omgeving met Hallo R-Script niet uitvoeren-module is geselecteerd.*

TooFigure 1 verwijst, bekijken we enkele van de belangrijkste onderdelen van Machine Learning Studio-omgeving voor het werken met Hallo HALLO hallo [R-Script uitvoeren] [ execute-r-script] module.

* Hallo-modules in Hallo-experiment worden in Hallo middelste deelvenster weergegeven.
* Hallo bovenste gedeelte van het rechter deelvenster Hallo bevat een venster tooview en uw R-scripts bewerken.  
* Hallo onderste gedeelte van het rechter deelvenster ziet u enkele eigenschappen van Hallo [R-Script uitvoeren][execute-r-script]. U kunt de logboeken van de fout en uitvoer van de Hallo weergeven door te klikken op de juiste plaatsen Hallo van dit deelvenster.

We zullen natuurlijk worden bespreken Hallo [R-Script uitvoeren] [ execute-r-script] in de rest van dit document Hallo uitgebreider.

Als u werkt met complexe R-functies, ik raden aan dat u bewerkt, testen en fouten in RStudio opsporen. Net als bij de ontwikkeling van alle software uw code stapsgewijs uitbreiden en het testen op kleine simpele testcases. Vervolgens knippen en plakken van uw functies in de script-venster Hallo R Hallo [R-Script uitvoeren] [ execute-r-script] module. Deze aanpak kunt u tooharness zowel Hallo RStudio integrated development environment (IDE) en kracht van Azure Machine Learning Hallo.  

#### <a name="execute-r-code"></a>R code uitvoeren
Geen R-code in Hallo [R-Script uitvoeren] [ execute-r-script] module wordt uitgevoerd wanneer u Hallo experiment uitvoeren door te klikken op Hallo **uitvoeren** knop. Wanneer de uitvoering is voltooid, een vinkje worden weergegeven op Hallo [R-Script uitvoeren] [ execute-r-script] pictogram.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Defensive R coderen voor Azure Machine Learning
Als u R-code voor, bijvoorbeeld een web-service ontwikkelt met behulp van Azure Machine Learning, moet u zeker plannen hoe uw code wordt omgaan met een onverwachte gegevensinvoer en uitzonderingen. toomaintain duidelijkheid ik niet opgenomen ongeveer Hallo manier van het controleren of de afhandeling van uitzonderingen in de meeste Hallo-codevoorbeelden die wordt weergegeven. Echter, als we gaan ik krijgt u enkele voorbeelden van functies met behulp van de mogelijkheid voor het verwerken van het R-uitzondering.  

Als u een uitgebreidere behandeling van R uitzonderingsverwerking moet, ik lezen van de betreffende gedeelten Hallo van Hallo boek door Wickham die worden vermeld in het beste [bijlage B - verdere lezen](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Debuggen en testen van R in Machine Learning Studio
tooreiterate, ik aanbevelen u testen en foutopsporing van uw R-code op kleine schaal in RStudio. Er zijn echter gevallen u waar tootrack omlaag R code problemen in Hallo moet [R-Script uitvoeren] [ execute-r-script] zelf. Bovendien is raadzaam om toocheck uw resultaten in Machine Learning Studio.

De uitvoer van Hallo uitvoering van uw R-code en op Hallo Azure Machine Learning platform is voornamelijk in uitvoer.log gevonden. Aanvullende informatie wordt weergegeven in error.log.  

Als een fout in Machine Learning Studio optreedt tijdens het uitvoeren van uw code R, moet uw eerste training van actie toolook op error.log. Dit bestand kan nuttig zijn fout berichten toohelp begrijpt en corrigeer de fout bevatten. tooview error.log, klik op **foutenlogboek weergeven** op Hallo **eigenschappendeelvenster** voor Hallo [R-Script uitvoeren] [ execute-r-script] met Hallo-fout.

Bijvoorbeeld: ik heb uitgevoerd Hallo na R-code met een niet-gedefinieerde variabele y in een [R-Script uitvoeren] [ execute-r-script] module:

    x <- 1.0
    z <- x + y

Deze code mislukt tooexecute, wat resulteert in een fout opgetreden. Te klikken op **foutenlogboek weergeven** op Hallo **eigenschappendeelvenster** produceert Hallo weergave wordt weergegeven in afbeelding 2.

  ![Foutbericht pop up][2]

*Afbeelding 2. Foutbericht pop-upvenster.*

Het lijkt erop dat we toolook uitvoer.log toosee Hallo R foutbericht weergegeven moet. Klik op Hallo [R-Script uitvoeren] [ execute-r-script] en klik vervolgens op Hallo **uitvoer.log weergeven** item op Hallo **eigenschappendeelvenster** toohello rechts. Hiermee opent u een nieuw browservenster en Zie Hallo volgende.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Dit foutbericht bevat geen verrassingen en duidelijk identificeert Hallo probleem.

tooinspect Hallo-waarde van een object in R, kunt u deze waarden toohello uitvoer.log bestand afdrukken. Hallo-regels voor het object onderzoek waarden zijn in wezen Hallo hetzelfde als in een interactieve R-sessie. Bijvoorbeeld, als u de naam van een variabele op een regel typt, Hallo waarde van Hallo object zal worden afgedrukt toohello uitvoer.log bestand.  

#### <a name="packages-in-machine-learning-studio"></a>Pakketten in Machine Learning Studio
Azure Machine Learning wordt geleverd met meer dan 350 vooraf geïnstalleerde R-taalpakketten. U kunt na de code in Hallo Hallo [R-Script uitvoeren] [ execute-r-script] module tooretrieve een lijst met Hallo vooraf geïnstalleerde pakketten.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Als u niet de laatste regel Hallo van deze code Hallo momenteel begrijpt, leest u op. In de rest van dit document Hallo behandeld uitvoerig R gebruiken in hello Azure Machine Learning-omgeving.

### <a name="introduction-toorstudio"></a>Inleiding tooRStudio
RStudio is een veelgebruikte IDE voor R. Ik gebruik RStudio bewerken, testen en foutopsporing aantal Hallo R-code die wordt gebruikt in deze snelstartgids. Zodra de R-code is getest en klaar zijn, u gewoon knippen en plakken van Hallo RStudio-editor naar een Machine Learning Studio [R-Script uitvoeren] [ execute-r-script] module.  

Als u geen Hallo R programmeertaal op uw computer geïnstalleerd, ik het beste dat u doet u dat nu. Gratis downloads van open-source R taal zijn beschikbaar op Hallo uitgebreide R archief netwerk (CRAN) op [http://www.r-project.org/](http://www.r-project.org/). Er zijn downloads beschikbaar voor Windows, Mac OS- en Linux/UNIX. Kies in de buurt mirror en volg Hallo downloaden aanwijzingen. CRAN bevat bovendien een schat aan nuttig analytics en data manipulatie pakketten.

Als u nieuwe tooRStudio, moet u downloaden en installeren van de bureaubladversie Hallo. U vindt Hallo die rstudio downloads voor Windows-, Mac OS- en Linux/UNIX op http://www.rstudio.com/products/RStudio/. Volg Hallo instructies tooinstall RStudio op uw computer.  

Een zelfstudie inleiding tooRStudio is beschikbaar op https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

Ik aanvullende informatie geven over het gebruik van RStudio in [bijlage A][appendixa].  

## <a id="scriptmodule"></a>Gegevens in en uit Hallo R-Script uitvoeren module ophalen
In deze sectie bespreken we hoe u gegevens ophalen van en naar Hallo [R-Script uitvoeren] [ execute-r-script] module. Wordt besproken hoe toohandle verschillende soorten gegevens lezen van en naar Hallo [R-Script uitvoeren] [ execute-r-script] module.

Hallo volledige code voor deze sectie wordt Hallo zip-bestand die u eerder hebt gedownload.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Laden en controleren van de gegevens in Machine Learning Studio
#### <a id="loading"></a>Hallo gegevensset laden
We wordt gestart door bij het laden van Hallo **csdairydata.csv** -bestand in Azure Machine Learning Studio.

* Start uw Azure Machine Learning Studio-omgeving.
* Klik op **+ nieuw** op Hallo linksonder van uw scherm en selecteer **gegevensset**.
* Selecteer **uit lokale bestand**, en vervolgens **Bladeren** tooselect Hallo-bestand.
* Zorg ervoor dat u hebt geselecteerd **generieke CSV-bestand met de header (.csv)** als type voor de gegevensset Hallo Hallo.
* Klik op het vinkje Hallo.
* Nadat Hallo gegevensset zijn geüpload, ziet u de nieuwe gegevensset Hallo door te klikken op Hallo **gegevenssets** tabblad.  

#### <a name="create-an-experiment"></a>Een experiment maken
Nu dat we enkele gegevens in Machine Learning Studio hebben, moeten we toocreate een experiment toodo Hallo analyse.  

* Klik op **+ nieuw** op Hallo linksonder loopt en selecteer **Experiment**, klikt u vervolgens **leeg Experiment**.
* Naam van uw experiment door te selecteren en te wijzigen, Hallo **Experiment op wordt gemaakt...**  titel bovenaan Hallo Hallo pagina. Bijvoorbeeld, te wijzigen**CA Zuivel Analysis**.
* Vouw op Hallo links van Hallo experiment pagina **gegevenssets opgeslagen**, en vervolgens **mijn gegevenssets**. U ziet Hallo **cadairydata.csv** die u eerder hebt geüpload.
* Slepen en neerzetten Hallo **csdairydata.csv gegevensset** op Hallo experiment.
* In Hallo **zoeken items experimenteren** vak op Hallo Hallo linkerdeelvenster type bovenaan [R-Script uitvoeren][execute-r-script]. Hier ziet u Hallo-module worden weergegeven in de zoeklijst Hallo.
* Slepen en neerzetten Hallo [R-Script uitvoeren] [ execute-r-script] module naar uw palet.  
* Verbinding maken met uitvoer Hallo Hallo **csdairydata.csv gegevensset** toohello meest linkse invoer (**Dataset1**) Hallo [R-Script uitvoeren][execute-r-script].
* **Vergeet niet tooclick op 'Save'.**  

Op dit moment ziet uw experiment er ongeveer als afbeelding 3.

![Hallo CA Zuivel Analysis experimenteren met de gegevensset en module R-Script uitvoeren][3]

*Afbeelding 3. Hallo CA Zuivel Analysis experimenteren met gegevensset en module R-Script niet uitvoeren.*

#### <a name="check-on-hello-data"></a>Controleer op Hallo-gegevens
We hebben bekijkt hello gegevens die we in ons experiment hebben geladen. Hallo-experiment, klik op Hallo uitvoer Hallo **cadairydata.csv gegevensset** en selecteer **visualiseren**. U ziet er ongeveer zo afbeelding 4.  

![Samenvatting van Hallo cadairydata.csv gegevensset][4]

*Afbeelding 4. Samenvatting van Hallo cadairydata.csv gegevensset.*

In deze weergave ziet u een groot aantal nuttige informatie. We zien Hallo eerste verschillende rijen van deze dataset. Als er een kolom selecteert, ziet u Hallo statistieken sectie meer informatie over het Hallo-kolom. Bijvoorbeeld, staan Hallo onderdeeltype rij ons welke gegevenstypen Azure Machine Learning Studio toohello kolom toegewezen. Een snelle zien er als volgt met is een goede controle, laten we toodo ernstige werk beginnen.

### <a name="first-r-script"></a>Eerste R-script
We maken met een eenvoudige eerste R-script tooexperiment met in Azure Machine Learning Studio. Ik heb gemaakt en getest Hallo script in RStudio te volgen.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Nu moet ik tootransfer dit script tooAzure Machine Learning Studio. Ik kan eenvoudig knippen en plakken. Echter, in dit geval ik draagt mijn R-script via een zip-bestand.

### <a name="data-input-toohello-execute-r-script-module"></a>Data-module voor invoer toohello R-Script uitvoeren
We hebben bekijkt hello invoer toohello [R-Script uitvoeren] [ execute-r-script] module. In dit voorbeeld wordt gelezen Hallo Californië melkkoeien gegevens in Hallo [R-Script uitvoeren] [ execute-r-script] module.  

Er zijn drie mogelijke ingangen voor Hallo [R-Script uitvoeren] [ execute-r-script] module. U kunt een of meer van deze invoer, afhankelijk van uw toepassing. Het is ook perfect redelijke toouse een R-script dat u helemaal geen invoer nodig.  

We bekijken op elk van deze invoerwaarden, van links tooright. Namen van elk van de invoerwaarden Hallo Hallo kunt u zien door de cursor op Hallo invoer plaatsen en Hallo knopinfo te lezen.  

#### <a name="script-bundle"></a>Script bundel
Hallo Script bundel invoer kunt u toopass Hallo inhoud van een zip-bestand in [R-Script uitvoeren] [ execute-r-script] module. U kunt een Hallo opdrachten tooread Hallo inhoud van het zip-bestand hello te volgen in uw R-code.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Azure Machine Learning bestanden in Hallo ZIP-bestand wordt behandeld alsof ze zich in Hallo src / Active directory, dus moet u de namen van het bestand met deze directorynaam tooprefix. Bijvoorbeeld, als hello zip Hallo bestanden bevat `yourfile.R` en `yourData.rdata` in de hoofdmap van de Hallo van Hallo zip, zou u deze poorten als adresseren `src/yourfile.R` en `src/yourData.rdata` bij gebruik van `source` en `load`.
> 
> 

Besproken al gegevenssets laden in [Hallo gegevensset laden](#loading). Zodra u hebt gemaakt en getest Hallo R-script wordt weergegeven in de vorige sectie hello, Hallo te volgen:

1. Sla Hallo R-script in een. R-bestand. Ik mijn scriptbestand 'simpleplot aanroepen. R'. Hier volgt Hallo inhoud.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Maak een zip-bestand en kopieer het script naar dit zipbestand. Op Windows, kunt u met de rechtermuisknop op het Hallo-bestand en selecteer **verzenden naar**, en vervolgens **gecomprimeerde map**. Hiermee maakt u een nieuwe zip-bestand met de Hallo 'simpleplot. R'-bestand.
3. Toevoegen van uw bestand toohello **gegevenssets** in Machine Learning Studio, geven Hallo type als **zip**. U ziet nu Hallo zip-bestand in de gegevenssets.
4. Slepen en neerzetten Hallo zip-bestand van **gegevenssets** op Hallo **ML Studio canvas**.
5. Verbinding maken met uitvoer Hallo Hallo **zip-gegevens** pictogram toohello **Script bundel** invoer Hallo [R-Script uitvoeren] [ execute-r-script] module.
6. Type Hallo `source()` functie met de naam van uw zip-bestand in het venster Hallo-code voor Hallo [R-Script uitvoeren] [ execute-r-script] module. Ik heb getypt in mijn geval `source("src/simpleplot.R")`.  
7. Controleer of u **opslaan**.

Als deze stappen voltooid zijn, Hallo [R-Script uitvoeren] [ execute-r-script] module Hallo R-script in Hallo zip-bestand wordt uitgevoerd wanneer Hallo experiment wordt uitgevoerd. Op dit moment ziet uw experiment er ongeveer als afbeelding 5.

![Experimenteer met gecomprimeerde R-script][6]

*Afbeelding 5. Experimenteer met gecomprimeerde R-script.*

#### <a name="dataset1"></a>Dataset1
U kunt een rechthoekig tabel gegevens tooyour R code doorgeven met behulp van Hallo Dataset1 invoer. In onze eenvoudig script Hallo `maml.mapInputPort(1)` functie Hallo gegevens leest uit poort 1. Deze gegevens worden vervolgens toegewezen tooa dataframe variabelenaam in uw code. In onze eenvoudig script voert de eerste coderegel Hallo Hallo-toewijzing.

    cadairydata <- maml.mapInputPort(1)

Uw experiment uitvoeren door te klikken op Hallo **uitvoeren** knop. Wanneer het Hallo-uitvoering is voltooid, klikt u op Hallo [R-Script uitvoeren] [ execute-r-script] module en klik vervolgens op **weergave logboek** op Hallo eigenschappendeelvenster. Een nieuwe pagina moet worden weergegeven in uw browser Hallo inhoud van Hallo uitvoer.log bestand weergegeven. Wanneer u omlaag schuiven ziet u dat lijkt op Hallo volgende.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Omlaag Hallo is verder pagina meer gedetailleerde informatie over het Hallo-kolommen als volgt Hallo volgende uitzien wordt.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

Deze resultaten zijn voornamelijk zoals verwacht, met 228 opmerkingen en 9 kolommen in Hallo dataframe. We zien kolomnamen hello, Hallo R-gegevenstype en een voorbeeld van elke kolom.

> [!NOTE]
> Deze dezelfde afdruk is gemakkelijk beschikbaar zijn via Hallo R-apparaat uitvoer Hallo [R-Script uitvoeren] [ execute-r-script] module. Bespreken we Hallo uitvoerwaarden van Hallo [R-Script uitvoeren] [ execute-r-script] module in de volgende sectie Hallo.  
> 
> 

#### <a name="dataset2"></a>Dataset2
Hallo is gedrag van Hallo Dataset2 invoer identiek toothat van Dataset1. U kunt met behulp van deze invoer een tweede rechthoekige gegevenstabel doorgeven in uw R-code. Hallo functie `maml.mapInputPort(2)`, wordt met Hallo argument 2, toopass gebruikt deze gegevens.  

### <a name="execute-r-script-outputs"></a>De uitvoer R-Script uitvoeren
#### <a name="output-a-dataframe"></a>Een dataframe uitvoer
Kunt u Hallo inhoud van een R-dataframe als een rechthoekig tabel via poort Hallo resultaat Dataset1 uitvoeren met behulp van Hallo `maml.mapOutputPort()` functie. In onze eenvoudig R-script wordt uitgevoerd door Hallo volgt regel.

    maml.mapOutputPort('cadairydata')

Klik op de uitvoerpoort resultaat Dataset1 Hallo na actieve Hallo-experiment, en klik vervolgens op **Visualize**. U ziet er ongeveer zo afbeelding 6.

![Hallo-visualisatie van uitvoer Hallo Hallo Californië melkkoeien gegevens][7]

*Afbeelding 6. Hallo visualisatie van uitvoer Hallo Hallo Californië melkkoeien gegevens.*

Deze uitvoer ziet er identiek toohello invoer, precies zoals verwacht.  

### <a name="r-device-output"></a>R-apparaat-uitvoer
Apparaat-uitvoer van Hallo Hallo [R-Script uitvoeren] [ execute-r-script] -module bevat de uitvoer van berichten en afbeeldingen. Beide standaard uitvoer en de standaardfout van R berichten worden toohello uitvoerpoort R-apparaat.  

tooview hello R-apparaat uitvoert, klik op Hallo-poort en klik vervolgens op **Visualize**. Hallo standaarduitvoer en de standaardfout van Hallo R-script in afbeelding 7 ziet.

![Standaarduitvoer en de standaardfout van Hallo poort R-apparaat][8]

*Afbeelding 7. Standaarduitvoer en de standaardfout van Hallo poort R-apparaat.*

We verschuift Zie Hallo grafische uitvoer van onze R-script in afbeelding 8.  

![Grafische uitvoer van Hallo poort R-apparaat][9]

*Afbeelding 8. Afbeeldingen de uitvoer van Hallo poort R-apparaat.*  

## <a id="filtering"></a>Gegevens filteren en transformatie
In deze sectie wordt uitgevoerd, er enkele elementaire gegevens filteren en transformatiebewerkingen op Hallo Californië melkkoeien gegevens. Hallo-einde van deze sectie hebben we gegevens in een indeling die geschikt is voor het bouwen van een analytische model.  

Meer specifiek, in deze sectie wordt we enkele algemene gegevens opruimen en transformatie taken uitvoeren: type transformatie, filteren op dataframes, nieuwe berekende kolommen, toe te voegen en de waarde van transformaties. Deze achtergrond kunt u veel variaties aangetroffen in de praktische problemen te maken met de Hallo.

Hallo volledige R-code voor deze sectie is beschikbaar in Hallo zip-bestand die u eerder hebt gedownload.

### <a name="type-transformations"></a>Type transformaties
Nu dat we Hallo Californië melkkoeien gegevens in de code in Hallo Hallo R lezen kan [R-Script uitvoeren] [ execute-r-script] -module, moeten we tooensure dat Hallo-gegevens in kolommen Hallo Hallo bedoeld type en de indeling heeft.  

R is een dynamisch getypeerde taal, wat betekent dat gegevenstypen worden gedwongen van één tooanother zoals vereist. Hallo-atomic gegevenstypen in R bevatten numerieke waarden, logische en -teken. Hallo factor type is gebruikte toocompactly categorische gegevens op te slaan. U vindt meer informatie over gegevenstypen in Hallo-verwijzingen in [bijlage B – Lees hier meer over](#appendixb).

Wanneer tabelgegevens wordt gelezen in R uit een externe bron, maar het is altijd een goed idee toocheck Hallo resulterende typen in Hallo kolommen. U kunt een kolom van het typeteken, maar in veel gevallen dit wordt weergegeven als factor of vice versa. In andere gevallen een kolom die u denkt dat moet worden wordt numerieke vertegenwoordigd door tekengegevens, bijvoorbeeld '1,23' in plaats van 1,23 als een zwevende-kommagetal.  

Gelukkig is eenvoudig tooconvert één type tooanother, zolang de toewijzing is mogelijk. Bijvoorbeeld, u 'Nevada' niet converteren naar een numerieke waarde, maar u tooa factor (categorische variabele) kunt converteren. U kunt bijvoorbeeld een numerieke 1 omzetten in een teken '1' of een factor.  

Hallo-syntaxis voor een van deze omzettingen is eenvoudig: `as.datatype()`. Deze functies voor typeconversie omvatten Hallo volgende.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Bekijkt hello gegevenstypen Hallo kolommen die we in de vorige sectie Hallo invoer: alle kolommen van het type numeriek zijn, met uitzondering van Hallo kolom met de naam 'Maand', van het typeteken is zijn. Laten we deze factor tooa converteren en Hallo testresultaten.  

Ik heb hebt Hallo-regel die Hallo scatterplot matrix gemaakt en een regel converteren Hallo 'Maand' kolom tooa factor toegevoegd verwijderd. In mijn experiment wordt ik net knippen en plakken Hallo R-code in het venster van de code Hallo Hallo [R-Script uitvoeren] [ execute-r-script] Module. U kunt ook Hallo zip-bestand bijwerken en tooAzure Machine Learning Studio te uploaden, maar verschillende stappen gaat.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Laten we deze code uitvoeren en bekijkt hello logboek voor Hallo R-script. Hallo relevante gegevens uit Hallo logboek wordt weergegeven in afbeelding 9.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Afbeelding 9. Samenvatting van Hallo dataframe met een factor-variabele.*

Hallo-type voor de maand nu de melding '**Factor met 14 niveaus**'. Dit is een probleem, omdat er alleen 12 maanden Hallo jaar. U kunt ook controleren toosee die type Hallo in **Visualize** Hallo resultaat gegevensset poort is '**Categorical**'.

Hallo-probleem is dat Hallo maand kolom heeft systematischer niet gecodeerd. In sommige gevallen een maand April wordt genoemd, en in andere gevallen wordt het april afgekort. We kunnen dit probleem oplossen door Hallo tekenreeks too3 tekens. Hallo volgende ziet coderegel Hallo nu:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Hallo-experiment opnieuw uitvoeren en Hallo logboek weergeven. Hallo verwacht resultaten worden weergegeven in afbeelding 10.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Afbeelding 10. Samenvatting van Hallo dataframe met het juiste aantal factorniveaus.*

Onze variabele factor heeft nu Hallo gewenst 12 niveaus.

### <a name="basic-data-frame-filtering"></a>Basisgegevens frame filteren
R dataframes ondersteunen krachtige filteropties. Gegevenssets kan subset met logische filters op rijen of kolommen zijn. In veel gevallen zijn complexe filtercriteria vereist. Hallo verwijzingen naar naamruimtes in [bijlage B – Lees hier meer over](#appendixb) uitgebreide voorbeelden voor het filteren van dataframes bevatten.  

Er is één bit van het filter moet worden uitgevoerd op onze gegevensset. Als u Hallo kolommen in Hallo cadairydata dataframe bekijkt, ziet u twee overbodige kolommen. de eerste kolom Hallo bevat alleen een rijnummer, niet erg nuttig is. Hallo tweede kolom Year.Month, bevat redundante gegevens. We kunnen deze kolommen eenvoudig uitsluiten door Hallo R code te volgen.

> [!NOTE]
> Vanaf nu op in deze sectie net leest u Hallo aanvullende code ik toe te in Hallo voegen [R-Script uitvoeren] [ execute-r-script] module. Ik zal elke nieuwe regel toevoegen **voordat** hello `str()` functie. Ik gebruik deze functie tooverify mijn resultaten in Azure Machine Learning Studio.
> 
> 

Ik toevoegen na toomy R coderegel in Hallo Hallo [R-Script uitvoeren] [ execute-r-script] module.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Deze code in uw experiment uitvoeren en controleren van Hallo resultaat uit Hallo-logboek voor uitvoer. Deze resultaten worden weergegeven in afbeelding 11.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Afbeelding 11. Samenvatting van Hallo dataframe met twee kolommen die zijn verwijderd.*

Goed nieuws! We ophalen Hallo verwacht resultaten.

### <a name="add-a-new-column"></a>Een nieuwe kolom toevoegen
toocreate time series modellen handige toohave een kolom met maanden sinds het starten van de tijdreeks Hallo HALLO hallo zal zijn. We gaan een nieuwe kolom 'Month.Count' maken.

toohelp Hallo-code maken we onze eerste eenvoudige functie organiseren `num.month()`. Deze functie toocreate een nieuwe kolom in Hallo dataframe wordt vervolgens toegepast. Hallo nieuwe code is als volgt.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

Nu Hallo bijgewerkt experiment uitvoeren en Hallo uitvoer logboek tooview Hallo resultaten gebruiken. Deze resultaten worden weergegeven in afbeelding 12.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Afbeelding 12. Samenvatting van Hallo dataframe met extra Hallo-kolom.*

Het lijkt dat alles werkt. De nieuwe kolom Hallo met Hallo verwachte waarden hebben we in ons dataframe.

### <a name="value-transformations"></a>Waarde transformaties
In deze sectie wordt we enkele eenvoudige transformaties op Hallo-waarden in een aantal Hallo kolommen van onze dataframe uitvoeren. Hallo R taal ondersteunt bijna willekeurige waarde transformaties. Hallo verwijzingen naar naamruimtes in [bijlage B - verdere lezen](#appendixb) uitgebreide voorbeelden bevatten.

Als u hello waarden in Hallo samenvattingen van onze dataframe bekijkt ziet u iets oneven hier. Is meer ijs dan melk geproduceerd in Californië? Nee, natuurlijk niet, omdat dit geen zin jammer als dit feit mogelijk toosome van ons ijs Ontwikkelaarshulpmiddelen. Hallo eenheden zijn verschillend. Er is een Hallo prijs in eenheden van ons pond, melk is in eenheden van 1 M VS pond, ijs in eenheden van 1000 ons gallon en Kwark in eenheden van 1000 VS pond is. Ervan uitgaande dat ijs weegt ongeveer 6,5 pond per gallon, kunnen we eenvoudig Hallo vermenigvuldiging tooconvert deze waarden, zodat ze allemaal in gelijk eenheden van 1000 pond.

We gebruiken een Multiplicatieve model voor het trendanalyse en correctie van deze gegevens voor onze prognosemodel. Een transformatie logboek kan we toouse een lineaire model, dit proces vereenvoudigen. Hallo logboek transformatie in dezelfde functie waarin Hallo vermenigvuldiger is toegepast Hallo kan worden toegepast.

Ik Definieer in Hallo code te volgen, een nieuwe functie `log.transform()`, en deze toohello rijen met Hallo numerieke waarden toe te passen. Hallo R `Map()` functie is gebruikte tooapply hello `log.transform()` functie toohello kolommen van Hallo dataframe geselecteerd. `Map()`lijkt te`apply()` maar kunt u meer dan een lijst met argumenten toohello functie. Opmerking dat een lijst met ze het tweede argument toohello Hallo levert `log.transform()` functie. Hallo `na.omit()` functie wordt gebruikt als een beetje van opschonen tooensure is er geen ontbreekt of niet-gedefinieerde waarden in Hallo dataframe.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

Er is zeer bits gebeurt in Hallo `log.transform()` functie. De meeste van deze code is controleren op mogelijke problemen met Hallo argumenten of omgaan met uitzonderingen die nog steeds tijdens het Hallo-berekeningen optreden kunnen. Slechts een paar regels van deze code daadwerkelijk Hallo berekeningen.

Hallo-doel van Hallo defensive programmering is tooprevent Hallo uitvallen van één functie die voorkomt dat de verwerking niet door kan gaan. Een plotselinge storing van een analyse langlopende kan frustrerend behoorlijk voor gebruikers. Deze situatie retourwaarden moeten worden gekozen die standaard wordt beperkt tooavoid toodownstream verwerking beschadigen. Een bericht is ook geproduceerde tooalert gebruikers die er iets verkeerd is geworden.

Als u niet gebruikte toodefensive programmering in R, zijn alle deze code lijkt enigszins overweldigend. Ik begeleidt u stapsgewijs door Hallo belangrijke stappen:

1. Een vector van vier berichten is gedefinieerd. Deze berichten zijn gebruikte toocommunicate informatie over een aantal Hallo mogelijke fouten en uitzonderingen die zich met deze code voordoen kunnen.
2. Ik retourneren NA de waarde voor elk geval. Er zijn tal van andere mogelijkheden die mogelijk minder neveneffecten hebben. Ik kan een vector uit nullen of Hallo oorspronkelijke invoer aanvalsvector, bijvoorbeeld retourneren.
3. Controles worden uitgevoerd op Hallo argumenten toohello functie. In elk geval als een fout wordt gedetecteerd, een standaardwaarde geretourneerd en wordt een bericht wordt geproduceerd door Hallo `warning()` functie. Ik gebruik `warning()` plaats `stop()` als laatste Hallo uitvoering beëindigt, precies wat ik probeer tooavoid. Houd er rekening mee dat ik hebt geschreven deze code in een procedurele style, zoals in dit geval een functionele benadering leek complex en verborgen.
4. Hallo logboek-berekeningen zijn samengevoegd in `tryCatch()` zodat uitzonderingen niet een abrupte stilstand tooprocessing tot leidt. Zonder `tryCatch()` de meeste fouten die worden gegenereerd door R functies resulteren in een stopsignaal ontvangen die geregeld worden.

Deze R-code in uw experiment uitvoeren en bekijkt hello uitvoer in Hallo uitvoer.log bestand afgedrukt. U ziet nu Hallo getransformeerd waarden Hallo vier kolommen in Hallo zich aanmeldt, zoals wordt weergegeven in afbeelding 13.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Afbeelding 13. Samenvatting van Hallo getransformeerd waarden in Hallo dataframe.*

We zien Hallo waarden zijn getransformeerd. Melkproductie nu is aanzienlijk groter dan alle andere melkkoeien product productie, terughalen dat we nu een logaritmische schaal kijkt.

Op dit moment onze gegevens wordt opgeschoond en we klaar zijn voor sommige modellen. Bekijkt hello visualisatie samenvatting voor Hallo resultaat gegevensset uitvoer van onze [R-Script uitvoeren] [ execute-r-script] -module, ziet u Hallo 'Maand' kolom 'Categorical' met 12 unieke waarden, weer is, net zoals we wilden .

## <a id="timeseries"></a>Time series-objecten en correlatieanalyse
In deze sectie we enkele eenvoudige R time series-objecten te verkennen en analyseren Hallo correlaties tussen sommige Hallo variabelen. Ons doel is een dataframe daarin Hallo pairwise correlatie informatie op verschillende lag toooutput.

Hallo volledige R-code voor deze sectie wordt Hallo zip-bestand die u eerder hebt gedownload.

### <a name="time-series-objects-in-r"></a>Time series-objecten in R
Zoals al is vermeld, tijd reeksen al een reeks gegevenswaarden geïndexeerd door tijd zijn. R time series-objecten zijn gebruikte toocreate en Hallo tijdsindex beheren. Er zijn enkele voordelen toousing time series-objecten. Time series-objecten vrij u van Hallo veel details van het beheer van Hallo reeks index tijdwaarden die worden ingekapseld in Hallo-object. Bovendien kunnen time series-objecten u toouse Hallo veel tijd reeks methoden voor het uitzetten, afdrukken, modellering, enzovoort.

Hallo POSIXct time series-klasse wordt vaak gebruikt en relatief eenvoudig is. Deze time series-klasse metingen tijd uit Hallo Hallo epoche, 1 januari 1970 is gestart. In dit voorbeeld gebruiken we POSIXct time series-objecten. Andere klassen gebruikte R time series-object zijn zoo en xts, uitbreidbare tijdreeks.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Voorbeeld van een reeks object tijd
Laten we aan de slag met het voorbeeld. Slepen en neerzetten een **nieuwe** [R-Script uitvoeren] [ execute-r-script] module in uw experiment. Verbinding maken met de uitvoerpoort Hallo resultaat Dataset1 van bestaande Hallo [R-Script uitvoeren] [ execute-r-script] module toohello Dataset1 invoer-poort van de nieuwe Hallo [R-Script uitvoeren] [ execute-r-script] module.

Zoals ik deed voor de eerste voorbeelden hello, als er voortgang via Hallo bijvoorbeeld op bepaalde tijdstippen leest alleen Hallo incrementele extra regels met R code bij elke stap.  

#### <a name="reading-hello-dataframe"></a>Hallo dataframe lezen
Als eerste stap gaan we lezen in een dataframe en controleer of dat we Hallo verwacht resultaten krijgt. Hallo volgende code moet doen Hallo-taak.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Voer nu Hallo experiment. Hallo-logboek van Hallo nieuwe R-Script uitvoeren vorm moet eruitzien als afbeelding 14.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*Afbeelding 14. Samenvatting van Hallo dataframe module Hallo R-Script niet uitvoeren.*

Deze gegevens zijn Hallo verwacht typen en opmaak. Houd er rekening mee dat het Hallo 'Maand' kolom van het type factor is en Hallo niveaus verwacht heeft.

#### <a name="creating-a-time-series-object"></a>Een time series-object maken
Er moet een time series-object tooour dataframe tooadd. De huidige code Hallo vervangen door Hallo volgende, waarmee een nieuwe kolom van klasse POSIXct worden toegevoegd.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

Controleer nu Hallo logboek. Het moet eruitzien als afbeelding 15.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Afbeelding 15. Samenvatting van Hallo dataframe met een time series-object.*

We zien van Hallo samenvatting dat die nieuwe Hallo-kolom is in feite van klasse POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Verkennen en Hallo gegevens transformeren
We gaan verkennen aantal Hallo variabelen in deze dataset. Een matrix scatterplot is een uitstekende manier tooproduce een beknopte beschrijving. Ik ben Hallo vervangen `str()` functie in de vorige R-code Hallo Hello volgt regel.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Voer deze code en kijk wat er gebeurt. Hallo tekent geproduceerd Hallo poort R-apparaat moet eruitzien als afbeelding 16.

![Matrix van geselecteerde variabelen Scatterplot][17]

*Afbeelding 16. Scatterplot matrix van geselecteerde variabelen.*

Er is een aantal vreemd uitziet structuur in Hallo relaties tussen deze variabelen. Misschien dit probleem doet zich van trends in Hallo gegevens en Hallo feit dat we hebben Hallo variabelen niet gestandaardiseerd.

### <a name="correlation-analysis"></a>Correlatieanalyse
tooperform correlatieanalyse moeten we tooboth ongedaan trend en standaardiseren Hallo-variabelen. Hallo R kan alleen worden gebruikt `scale()` functie, die zowel datacenters en het schalen van variabelen. Deze functie mogelijk ook sneller worden uitgevoerd. Echter, ik wil dat tooshow u een voorbeeld van defensive programing in R.

Hallo `ts.detrend()` functie hieronder beide van deze bewerkingen uitvoert. Hallo volgende twee regels code ongedaan trend Hallo gegevens en vervolgens standaardiseren Hallo waarden.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

Er is zeer bits gebeurt in Hallo `ts.detrend()` functie. De meeste van deze code is controleren op mogelijke problemen met Hallo argumenten of omgaan met uitzonderingen die nog steeds tijdens het Hallo-berekeningen optreden kunnen. Slechts een paar regels van deze code daadwerkelijk Hallo berekeningen.

We hebben al een voorbeeld van defensive programmering in besproken [transformaties waarde](#valuetransformations). Beide blokken berekening zijn samengevoegd in `tryCatch()`. Voor een aantal fouten op deze manier zin tooreturn Hallo oorspronkelijke invoer vector en in andere gevallen ik een vector nullen retourneren.  

Houd er rekening mee dat Hallo lineaire regressie gebruikt voor trending ongedaan een reeks tijd regressie. Hallo manier variabele is een time series-object.  

Eenmaal `ts.detrend()` is gedefinieerd we deze toe te passen toohello variabelen in onze dataframe van belang. We moeten de resulterende lijst Hallo gemaakt door forceren `lapply()` toodata dataframe met behulp van `as.data.frame()`. Vanwege defensive aspecten van `ts.detrend()`, fout tooprocess een van de variabelen Hallo voorkomt niet dat corrigeren verwerking van Hallo anderen.  

Hallo laatste regel van code maakt een pairwise scatterplot. Hallo-resultaten van Hallo scatterplot worden na het uitvoeren van Hallo R code weergegeven in afbeelding 17.

![Pairwise scatterplot van ongedaan trendanalyse en gestandaardiseerde tijdreeks][18]

*Afbeelding 17. Pairwise scatterplot van ongedaan trendanalyse en gestandaardiseerde tijdreeks.*

U kunt deze resultaten toothose weergegeven in afbeelding 16 vergelijken. Hello trend verwijderd en variabelen gestandaardiseerd Hallo zien we veel minder structuur in Hallo relaties tussen deze variabelen.

Hallo code toocompute Hallo correlaties als R ccf objecten is als volgt.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

Deze code wordt weergegeven in afbeelding 18 Hallo-logboek.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*Afbeelding 18. Lijst met ccf objecten uit Hallo pairwise correlatieanalyse.*

Er is een waarde voor correlation voor elke vertraging. Geen van deze waarden correlatie is groot genoeg toobe aanzienlijke. We kunnen daarom sluiten we elke variabele onafhankelijk kunnen model.

### <a name="output-a-dataframe"></a>Een dataframe uitvoer
We hebben Hallo pairwise correlaties berekend als een lijst met R ccf objecten. Dit vormt een bits van een probleem als resultaat gegevensset uitvoerpoort Hallo echt een dataframe vereist. Bovendien Hallo ccf object zelf een lijst en willen we alleen Hallo waarden in het eerste element van deze lijst, Hallo correlaties op Hallo Hallo verschillende lag.

Hallo code uitgepakt Hallo lag waarden uit de lijst Hallo ccf objecten, die zelf een lijst met te volgen.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

de eerste coderegel Hallo iets lastig is en een verklaring waarmee u inzicht. Hallo door werken hebben we Hallo volgende:

1. Hallo '**[[**'operator met Hallo argument'**1**' worden geselecteerd Hallo vector van correlaties op Hallo vertragingen bij het berekenen van Hallo eerste element van Hallo ccf objectenlijst.
2. Hallo `do.call()` functie is van toepassing hello `rbind()` functie via Hallo elementen van Hallo lijst retourneert door `lapply()`.
3. Hallo `data.frame()` functie koppelt Hallo resultaat geproduceerd door `do.call()` tooa dataframe.

Houd er rekening mee dat Hallo rijnamen in een kolom van Hallo dataframe zijn. In dat geval Hallo rijnamen behouden blijft wanneer ze de uitvoer van Hallo [R-Script uitvoeren][execute-r-script].

Hallo-code wordt weergegeven in afbeelding 19 Hallo-uitvoer wanneer ik **Visualize** Hallo uitvoer op Hallo resultaat gegevensset poort. Hallo rijnamen zijn in de eerste kolom hello, zoals bedoeld.

![Uitvoer van de resultaten van Hallo correlatieanalyse][20]

*Afbeelding 19. Resultaten de uitvoer van Hallo correlatieanalyse.*

## <a id="seasonalforecasting"></a>Time series-voorbeeld: seizoensgebonden prognose
Onze gegevens is nu in een formulier dat geschikt is voor analyse en we hebben vastgesteld dat er zijn geen belangrijke correlatie tussen het Hallo-variabelen. We gaan en maken van een tijdreeks prognose model. Met dit model wordt we forecast Californië melkproductie voor Hallo 12 maanden van 2013.

Onze prognosemodel heeft twee componenten, een onderdeel van het trendanalyse en een seizoen onderdeel. Hallo voltooid prognose is Hallo product van deze twee componenten. Dit type model staat bekend als een Multiplicatieve model. Hallo alternatief is een additieve model. We hebben al een logboek transformatie toohello variabelen van belang, waardoor deze analyse tractable toegepast.

Hallo volledige R-code voor deze sectie wordt Hallo zip-bestand die u eerder hebt gedownload.

### <a name="creating-hello-dataframe-for-analysis"></a>Hallo dataframe voor analyse maken
Voeg eerst een **nieuwe** [R-Script uitvoeren] [ execute-r-script] module tooyour experiment. Verbinding maken met de Hallo **resultaat gegevensset** uitvoer van de bestaande Hallo [R-Script uitvoeren] [ execute-r-script] module toohello **Dataset1** invoer van de nieuwe module Hallo. Hallo resultaat ziet er ongeveer als afbeelding 20.

![Hallo experimenteren met Hallo nieuwe R-Script uitvoeren module toegevoegd][21]

*Afbeelding 20. Hallo experimenteren met Hallo nieuwe R-Script uitvoeren module toegevoegd.*

Als met Hallo correlatie analyses die we zojuist, moeten we tooadd een kolom met een POSIXct time series-object. Hallo volgende code wordt hiervoor alleen.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Voer deze code en bekijkt hello logboek. Hallo resultaat moet eruitzien als afbeelding 21.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Afbeelding 21. Een samenvatting van Hallo dataframe.*

Met dit resultaat we klaar toostart zijn onze analyse.

### <a name="create-a-training-dataset"></a>Maken van een gegevensset training
We moeten toocreate een gegevensset met de training met Hallo dataframe samengesteld. Deze gegevens omvatten alle Hallo opmerkingen, behalve de afgelopen 12, van Hallo jaar 2013, Hallo die onze testgegevensset is. Hallo volgende subsets Hallo dataframe code en curve van Hallo melkkoeien productie- en variabelen maakt. Ik vervolgens curve van Hallo vier productie- en variabelen maken. Anonieme functie gebruikte toodefine is sommige verbetert voor tekengebied en vervolgens doorlopen Hallo lijst Hallo andere twee argumenten met `Map()`. Als u denkt u zijn die een voor de lus zou hebt gewerkt probleemloos hier, u juist zijn. Maar aangezien R is een functionele taal ik ben waarin u een functionele benadering.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

Hallo-code wordt Hallo reeks tijdreeks van Hallo R-apparaat uitvoer weergegeven in afbeelding 22 grafieken. Houd er rekening mee dat tijdas Hallo in eenheden van datums nice voordeel van het Hallo-tijd reeks methode tekenen.

![Eerste dag van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Tweede van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Derde van de time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Vierde van time series curve van Californië melkkoeien productie- en -gegevens](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Afbeelding 22. Time series curve van Californië zuivelproductie en gegevens voor de prijs.*

### <a name="a-trend-model"></a>Een model trend
Een time series-object en bekijkt hello gegevens heeft gehad dat het gemaakt, begint tooconstruct een model trend voor Hallo Californië melk productiegegevens. We kunnen dit doen met een reeks tijd regressie. Het is echter wissen uit Hallo tekent dat we wordt moet meer dan een tooaccurately richting en snijpunt model Hallo trend in Hallo trainingsgegevens waargenomen.

Op kleine schaal Hallo Hallo gegevens opgegeven, ik zal Hallo-model voor de trend in RStudio maken en vervolgens knippen en plakken Hallo resulterende model in Azure Machine Learning. RStudio biedt een interactieve omgeving voor dit type interactieve analyses.

Als een eerste poging probeer ik een polynomiale regressie met bevoegdheden up too3. Er is een echte gevaar voor dit soort modellen te veel aanpassen. Daarom is het beste tooavoid hoge voorwaarden. Hallo `I()` functie belemmert interpretatie van Hallo-inhoud (interpreteert Hallo inhoud 'omdat'), en kunt u een letterlijk geïnterpreteerde functie toowrite in een regressievergelijking.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Hiermee wordt de volgende Hallo gegenereerd.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

Van P-waarden (Pr (> | t |)) in deze uitvoer kunt zien we dat Hallo mogelijk aanzienlijke gekwadrateerde term niet. Ik gebruik Hallo `update()` toomodify dit model door weggehaald Hallo term kwadraat werken.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Hiermee wordt de volgende Hallo gegenereerd.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

Dit ziet er beter. Alle Hallo voorwaarden zijn van belang. Hallo 2e-16-waarde is echter een standaardwaarde, en moet niet ernstig te worden genomen.  

Als een test sanity time series tekent Hallo Californië zuivelproductie gegevens we te maken met Hallo trend curve weergegeven. Ik heb de volgende code in Azure Machine Learning Hallo Hallo toegevoegd [R-Script uitvoeren] [ execute-r-script] model (geen RStudio) toocreate Hallo model en tekent maken. Hallo resultaat wordt weergegeven in afbeelding 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Californië melk productiegegevens met trend model weergegeven](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Afbeelding 23. Californië melk trend model weergegeven met productiegegevens.*

Lijkt Hallo trend model Hallo gegevens vrij goed past. Bovendien wordt lijkt er niet toobe bewijs van te veel aanpassen zoals oneven wiggles in Hallo model curve.  

### <a name="seasonal-model"></a>Seizoensgebonden model
Een model van de trend in de hand, we toopush op moet en Hallo seizoensgebonden gevolgen zijn. Hallo maand van het Hallo jaar zullen worden gebruikt als een dummy-variabele Hallo lineair model toocapture Hallo per maand gelden. Houd er rekening mee dat wanneer u factor variabelen in een model introduceren, Hallo intercept moet niet worden berekend. Als u dit niet hebt, Hallo formule is te veel opgegeven R beëindigt een Hallo factoren gewenst maar Hallo intercept term houden.

Aangezien we een model tevredenheid trend hebben we Hallo kunt gebruiken `update()` functie tooadd Hallo nieuwe termen toohello bestaande model. Hallo -1 in Hallo update formule zakt Hallo intercept term. Als u doorgaat in RStudio voor Hallo moment:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Hiermee wordt de volgende Hallo gegenereerd.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

Ziet u dat model Hallo niet langer een term intercept heeft en 12 maand belangrijke factoren. Dit is precies wilden we toosee.

We maken een andere tijd reeks tekent van Hallo Californië zuivelproductie gegevens toosee hoe goed Hallo seizoensgebonden model werkt. Ik heb de volgende code in Azure Machine Learning Hallo Hallo toegevoegd [R-Script uitvoeren] [ execute-r-script] toocreate Hallo model en tekent maken.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Deze code uitgevoerd in Azure Machine Learning produceert Hallo grafiek wordt weergegeven in afbeelding 24.

![Californië melkproductie met model inclusief seizoensgebonden effecten](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Afbeelding 24. Melkproductie Californië met model inclusief seizoensgebonden gevolgen.*

Hallo is aanpassen toohello gegevens weergegeven in afbeelding 24 in plaats van te bevorderen. Hallo trend zowel Hallo invloed (maandelijks variatie) Zoek redelijke.

Als een nieuwe controle uit op het model, gaan we hebben bekijkt hello verschillen opgeven. Hallo berekent de volgende code Hallo voorspelde waarden uit onze twee modellen, Hallo verschillen opgeven voor de seizoensgebonden model hello wordt berekend en vervolgens deze verschillen opgeven voor de trainingsgegevens Hallo worden uitgezet.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

Hallo achtergebleven grafiek wordt weergegeven in afbeelding 25.

![Verschillen van de seizoensgebonden model Hallo voor Hallo trainingsgegevens opgeven](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Afbeelding 25. Als u dit van Hallo seizoensgebonden model voor Hallo trainingsgegevens.*

Deze verschillen opgeven zoeken redelijke. Er is geen specifieke structuur, met uitzondering van Hallo effect van Hallo 2008-2009 recessie, die het model wordt geen rekening gehouden met name goed.

Hallo-grafiek wordt weergegeven in afbeelding 25 is nuttig voor het detecteren van alle tijdsafhankelijke patronen in Hallo verschillen opgeven. Hallo expliciete benadering van computer- en uitzetten Hallo dit die ik gebruikt plaatst Hallo verschillen opgeven in volgorde van de tijd op Hallo tekent. Als op Hallo daarentegen ik had uitgezet `milk.lm$residuals`, Hallo tekent zou zijn niet in volgorde van de tijd.

U kunt ook `plot.lm()` tooproduce een reeks diagnostische waarnemingspunten.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Deze code wordt een reeks diagnostische waarnemingspunten wordt weergegeven in afbeelding 26 geproduceerd.

![Eerste dag van diagnostische waarnemingspunten voor het seizoen Hallo-model](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Tweede van diagnostische waarnemingspunten voor Hallo seizoensgebonden model](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Derde van diagnostische waarnemingspunten voor het seizoen Hallo-model](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Vierde van diagnostische waarnemingspunten voor Hallo seizoensgebonden model](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Afbeelding 26. Diagnose worden uitgezet voor Hallo seizoensgebonden model.*

Er zijn een aantal maximaal invloedrijke punten in deze waarnemingspunten, maar niets geïdentificeerd toocause geweldige zorgen. Bovendien ziet u van Hallo normaal Q-Q tekent dat dit Hallo sluiten toonormally gedistribueerd, belangrijke verondersteld voor lineaire modellen zijn.

### <a name="forecasting-and-model-evaluation"></a>Prognosemodel en model evalueren
Er is slechts één meer ding toodo toocomplete ons voorbeeld. We moet toocompute prognoses en Hallo fout tegen Hallo actuele gegevens te meten. Onze prognose worden voor Hallo 12 maanden van 2013. We kunt een meting fout voor deze prognose toohello feitelijke gegevens die geen deel uitmaakt van onze gegevensset training berekenen. Daarnaast kunnen we vergelijken de prestaties van Hallo 18 jaar training gegevens toohello 12 maanden van testgegevens.  

Een aantal metrische gegevens gebruikt toomeasure Hallo prestaties van de time series-modellen. In ons geval gebruiken we Hallo root mean vierkant (RMS)-fout. Hallo berekent volgende functie Hallo RMS fout tussen twee reeksen.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Net als bij Hallo `log.transform()` functie besproken in sectie 'Transformaties waarde' hello, wordt er zeer veel fout controleren en uitzondering code voor herstel in deze functie. Hallo principes werkzaam zijn Hallo dezelfde. Hallo werk wordt uitgevoerd op twee plaatsen die zijn ingepakt `tryCatch()`. Hallo tijdreeks zijn eerst exponentiated, omdat we hebt gewerkt met Hallo logboeken van Hallo waarden. Ten tweede wordt Hallo werkelijke RMS fout berekend.  

Uitgerust met een functie toomeasure Hallo RMS-fout, gaan we bouwen en de uitvoer een dataframe met Hallo RMS fouten. Nemen we voorwaarden voor Hallo trend model alleen en Hallo volledig model met seizoensgebonden factoren. Hallo volgende code Hallo taak met behulp van Hallo twee lineaire modellen die we hebt gemaakt.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

Deze code wordt Hallo-uitvoer die wordt weergegeven in afbeelding 27 op Hallo uitvoerpoort resultaat gegevensset.

![Vergelijking van RMS-fouten voor Hallo modellen][26]

*Afbeelding 27. Vergelijking van RMS-fouten voor Hallo-modellen.*

Van deze resultaten ziet u dat toe te voegen Hallo seizoensgebonden factoren toohello model Hallo RMS-fout aanzienlijk vermindert. Te heten dan Hallo RMS-fout voor Hallo training gegevens een bits kleiner is dan voor Hallo prognose.

## <a id="appendixa"></a>BIJLAGE A: Handleiding tooRStudio
RStudio heel goed wordt gedocumenteerd, zodat in deze bijlage ik bieden sommige koppelingen toohello sleutel secties van Hallo RStudio documentatie tooget die u gestart.

1. Projecten maken
   
   U kunt ordenen en beheren van uw R-code in de projecten via RStudio. Hallo-documentatie die gebruikmaakt van de projecten kan worden gevonden op https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   Ik het beste als volgt uit te voeren en maak een project voor Hallo R-codevoorbeelden in dit document.  
2. Bewerken en het uitvoeren van R-code
   
   RStudio biedt een geïntegreerde omgeving voor het bewerken en R-code wordt uitgevoerd. Documentatie vindt u op https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Foutopsporing
   
   RStudio omvat krachtige mogelijkheden voor foutopsporing. Documentatie voor deze functies is op https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   Hallo onderbrekingspunt voor probleemoplossing functies zijn tijdens https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting gedocumenteerd.

## <a id="appendixb"></a>BIJLAGE B: Lees hier meer over
Deze zelfstudie behandelt Hallo basisbeginselen programming R van wat u moet toouse Hallo R taal met Azure Machine Learning Studio. Als u niet bekend met R bent, zijn twee inleidingen beschikbaar op CRAN:

* R voor beginnende gebruikers door Emmanuel Paradis is een goede plaats toostart op http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* Een rondleiding inleiding door W. N. Venables et. al. in iets meer diepte op http://cran.r-project.org/doc/manuals/R-intro.html gaan.

Er zijn veel books op R waarmee u aan de slag kunt. Hier volgen enkele die ik handig:

* Hallo illustraties van R Programming: een rondleiding van statistische softwareontwerp door Norman Matloff is een uitstekende inleiding tooprogramming in R.  
* R Cookbook door Paul Teetor biedt een probleem en oplossing benadering toousing R.  
* R in actie door Robert Kabacoff is een ander nuttig inleidende rapport. Hallo companion snelle R website is een nuttig resource op http://www.statmethods.net/.
* R Inferno door Patrick Burns is een verrassend grappige boek dat met een aantal lastig en moeilijk onderwerpen die kan worden gevonden werkt bij het programmeren in R. Hallo boek is beschikbaar voor het vrije op http://www.burns-stat.com/documents/books/the-r-inferno/.
* Als u wilt dat een diepgaand in geavanceerde onderwerpen in R, hebt u bekijkt hello adresboek Geavanceerd R door Hadley Wickham. Hallo onlineversie van deze handleiding is beschikbaar voor het vrije op http://adv-r.had.co.nz/.

Een lijst van R time series-pakketten kunt u vinden in Hallo CRAN taakweergave voor analyse van reeks: http://cran.r-project.org/web/views/TimeSeries.html. Voor informatie over een specifiek tijdstip reeks object pakketten raadpleegt u toohello-documentatie voor dit pakket.

Hallo adresboek inleidende Time Series met R door Paul Cowpertwait en Andrew Metcalfe biedt een inleiding toousing R voor analyse van reeks. Veel meer theoretische teksten bevatten R voorbeelden.

Sommige geweldige internetbronnen:

* DataCamp: DataCamp leert R Hallo deur uit uw browser met video uitkomsten en codering oefeningen. Er zijn interactieve zelfstudies op Hallo nieuwste R technieken en pakketten. Hallo gratis interactieve R zelfstudie bij https://www.datacamp.com/courses/introduction-to-r worden
* Een handleiding op aan de slag met R van Programiz https://www.programiz.com/r-programming
* Een snelle zelfstudie van R door Kelly Black van Clarkson universiteit http://www.cyclismo.org/tutorial/R/
* 60 + R-resources die wordt vermeld op http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
