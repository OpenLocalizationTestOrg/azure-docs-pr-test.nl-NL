---
title: aaaData wetenschappelijke op Hallo Linux gegevens wetenschappelijke virtuele Machine | Microsoft Docs
description: Hoe tooperform enkele algemene gegevenswetenschap taken Hello Linux gegevens wetenschappelijke VM.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Gegevenswetenschap op Hallo Linux gegevens wetenschappelijke virtuele Machine
Dit overzicht toont u hoe tooperform enkele algemene gegevenswetenschap taken Hello Linux gegevens wetenschappelijke VM. Hallo Linux gegevens wetenschappelijke virtuele Machine (DSVM) is beschikbaar in Azure die vooraf worden geïnstalleerd met een verzameling hulpprogramma's die doorgaans gebruikt voor gegevensanalyse en machine learning op de installatiekopie van een virtuele machine. Hallo belangrijke software-onderdelen worden gespecificeerd in Hallo [inrichten Hallo Linux gegevens wetenschappelijke virtuele Machine](machine-learning-data-science-linux-dsvm-intro.md) onderwerp. Hallo VM-installatiekopie maakt het eenvoudig tooget gestart tijdens het doorzoeken van wetenschappelijke gegevens in minuten, zonder tooinstall en elk van de hulpprogramma's voor Hallo afzonderlijk configureren. U kunt eenvoudig opschalen Hallo VM, indien nodig en stop de toepassing als deze niet in gebruik. Deze resource wordt dus elastische en betaalbare.

Hallo gegevens wetenschappelijke taken gedemonstreerd in dit overzicht stappen Hallo die worden beschreven in Hallo [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Deze procedure biedt een systematisch toodata wetenschappelijke waarmee teams van gegevenswetenschappers tooeffectively via Hallo levenscyclus van het bouwen van intelligente toepassingen samenwerken. Hallo gegevens wetenschap proces biedt ook een iteratieve framework voor gegevenswetenschap die kan worden gevolgd door een persoon.

Analyseren we Hallo [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) gegevensset in dit scenario. Dit is een set van e-mailberichten die zijn gemarkeerd als spam of ham (wat betekent dat ze zijn geen spam), en het bevat ook een aantal statistieken Hallo inhoud van het Hallo-e-mailberichten. Hallo statistieken opgenomen worden besproken in Hallo naast maar één sectie.

## <a name="prerequisites"></a>Vereisten
Voordat u een virtuele Machine voor Linux gegevens wetenschappelijke gebruiken kunt, moet u de volgende Hallo hebben:

* Een **Azure-abonnement**. Als u nog geen een, Zie [maken van uw gratis Azure-account vandaag](https://azure.microsoft.com/free/).
* Een [ **gegevenswetenschap Linux VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Zie voor meer informatie over het inrichten van deze virtuele machine [inrichten Hallo Linux gegevens wetenschappelijke virtuele Machine](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) geïnstalleerd op uw computer en een XFCE-sessie hebt geopend. Voor informatie over het installeren en configureren van een **X2Go client**, Zie [installeren en configureren van de client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* Een **AzureML account**. Als u nog geen hebt, zich aanmelden voor een nieuw wachtwoord op Hallo [AzureML-startpagina](https://studio.azureml.net/). Er is een gratis gebruik laag toohelp die u aan de slag.

## <a name="download-hello-spambase-dataset"></a>Hallo spambase gegevensset downloaden
Hallo [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) gegevensset is een relatief klein set gegevens die alleen 4601 voorbeelden bevat. Dit is een handige grootte toouse wanneer dat sommige van de belangrijkste functies van de Hallo Hallo gegevens wetenschappelijke VM zoals deze houdt Hallo resourcevereisten matige te demonstreren.

> [!NOTE]
> In dit scenario is gemaakt op een D2 v2-formaat Linux gegevens wetenschappelijke virtuele Machine. Deze grootte DSVM kan afhandelen Hallo procedures in dit scenario is.
>
>

Als u meer opslagruimte nodig hebt, kunt u extra schijven maken en deze tooyour VM koppelt. Deze schijven gebruiken een permanente Azure-opslag, zodat hun gegevens behouden blijven zelfs wanneer het Hallo-server is ingericht vanwege tooresizing of wordt afgesloten. tooadd een schijf en koppelt u dit tooyour VM, volg de instructies in Hallo [toevoegen van een schijf tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Deze stappen hello Azure-opdrachtregelinterface (Azure CLI), die al is geïnstalleerd op Hallo DSVM gebruiken. Deze procedures is dus mogelijk volledig uit Hallo VM zelf. Een andere optie tooincrease opslag is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).

toodownload hello gegevens, open een terminalvenster en voer deze opdracht uit:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

het gedownloade bestand Hallo niet hebben een veldnamenrij, dus we maken een ander bestand dat u beschikt over een koptekst. Voer deze opdracht toocreate een bestand met de juiste kopteksten Hallo:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Vervolgens samenvoegen van Hallo twee bestanden samen met de Hallo-opdracht:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

Hallo gegevensset heeft verschillende typen statistieken op elk e-mailbericht:

* Kolommen, zoals ***word\_freq\_WORD*** geven Hallo percentage woorden in Hallo e-mail die overeenkomen met *WORD*. Bijvoorbeeld, als *word\_freq\_zorg* is 1, wordt 1% van alle woorden in Hallo e-mailbericht zijn *zorg*.
* Kolommen, zoals ***char\_freq\_CHAR*** geven Hallo percentage van alle tekens in Hallo e-mailbericht zijn *CHAR*.
* ***kapitaal\_uitvoeren\_lengte\_langste*** is Hallo langste lengte van een reeks van hoofdletters.
* ***kapitaal\_uitvoeren\_lengte\_gemiddelde*** Hallo gemiddelde duur van alle reeksen hoofdletters is.
* ***kapitaal\_uitvoeren\_lengte\_totale*** Hallo totale lengte van alle reeksen hoofdletters is.
* ***spam*** geeft aan of e-mail hello wordt beschouwd als spam of niet (1 = spam, 0 = niet spam).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Hallo gegevensset met Microsoft R Open verkennen
Laten we Hallo gegevens controleren en voer enkele eenvoudige machine learning R. Hello gegevens wetenschappelijke VM wordt geleverd met [Microsoft R Open](https://mran.revolutionanalytics.com/open/) vooraf zijn geïnstalleerd. Hallo bieden multithreaded math bibliotheken in deze versie van R betere prestaties dan in verschillende versies met één thread. Microsoft R Open biedt ook reproduceerbaarheid met behulp van een momentopname van Hallo CRAN pakket opslagplaats.

tooget kopieën van Hallo codevoorbeelden in dit scenario, kloon Hallo gebruikt **Azure-Machine-Learning--Gegevenswetenschap** opslagplaats met git, dat vooraf is geïnstalleerd op Hallo VM. Voer vanaf Hallo git-opdrachtregel:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Open een terminalvenster en een nieuwe R-sessie starten met Hallo R interactieve console.

> [!NOTE]
> U kunt ook RStudio gebruiken voor Hallo procedures te volgen. tooinstall RStudio, geef dan deze opdracht in een terminal:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

tooimport hello gegevens en stelt u de omgeving hello, uitvoeren:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee samenvattende statistieken over elke kolom:

    summary(data)

Voor een andere weergave van Hallo gegevens:

    str(data)

Dit toont u type van elke variabele Hallo en Hallo eerst enkele waarden in Hallo gegevensset.

Hallo *spam* kolom als een geheel getal is gelezen, maar het is daadwerkelijk een categorische variabele (of factor). tooset het type:

    data$spam <- as.factor(data$spam)

toodo sommige experimentele analyses, gebruik Hallo [ggplot2](http://ggplot2.org/) inpakken, een populaire grafische-bibliotheek voor R dat al is geïnstalleerd op Hallo VM. Opmerking van Hallo samenvattingsgegevens dat eerder is weergegeven, dat we samenvattende statistieken op Hallo frequentie van Hallo uitroepteken teken hebben. Laten we deze frequenties hier tekenen Hello volgende opdrachten:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Aangezien Hallo nul balk Hallo tekent scheeftrekken wordt, gaan we deze verwijderen uit:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Er is een niet-triviale dichtheid dan 1, waarin u geïnteresseerd. Bekijk alleen die gegevens in:

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Vervolgens splitsen door spam tegenover ham:

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Deze voorbeelden moeten u in staat stellen toomake vergelijkbare curve van Hallo andere kolommen tooexplore Hallo in deze gegevens.

## <a name="train-and-test-an-ml-model"></a>Trainen en te testen ML-model
Nu gaan we trein een aantal machine learning tooclassify Hallo e-mailberichten in Hallo gegevensset modellen bevat een span of ham. We een decision tree-model en een willekeurige forest-model in deze sectie trainen en vervolgens de juistheid van hun voorspellingen.

> [!NOTE]
> Hallo rpart (recursieve partitioneren en Regressiestructuren)-pakket gebruikt in de volgende code Hallo is al geïnstalleerd op Hallo gegevens wetenschappelijke VM.
>
>

Eerst laten we Hallo gegevensset splitsen in trainings- en testset sets:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

En maak vervolgens een decision tree tooclassify Hallo e-mailberichten.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Hier volgt Hallo resultaat:

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

hoe goed worden uitgevoerd op Hallo training toodetermine ingesteld, Hallo volgende code gebruiken:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

toodetermine hoe goed worden uitgevoerd op Hallo testset:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

U kunt ook gaan we een willekeurige forest-model. Willekeurige forests tal van beslissingsstructuren trainen en uitvoer van een klasse die Hallo-modus van Hallo classificaties uit alle Hallo afzonderlijke beslissingsstructuren. Ze bieden een krachtigere machine learning-benadering als voor de neiging Hallo van een decision tree model toooverfit een gegevensset training worden gecorrigeerd.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Een model tooAzure ML implementeren
[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is een cloudservice die maakt het eenvoudig toobuild en implementeren van predictive analytics-modellen. Een van de Hallo nice functies van AzureML is de mogelijkheid toopublish R functioneren als een webservice. Hallo AzureML-R-pakket maakt implementatie eenvoudig toodo vanaf onze R-sessie op Hallo DSVM.

toodeploy hello besluit structuur code uit de vorige sectie hello, moet u toosign in tooAzure Machine Learning Studio. U moet uw werkruimte-ID en een token toosign autorisatie in. toofind deze waarden en geïnitialiseerd Hallo AzureML variabelen met hen:

Selecteer **instellingen** Hallo links menu. Opmerking uw **WERKRUIMTE-ID**. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Selecteer **autorisatie Tokens** uit Hallo overhead menu en Opmerking uw **primaire autorisatie Token**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Load Hallo **AzureML** van het pakket en stelt u waarden van variabelen Hallo met uw token en werkruimte-ID in uw R-sessie op Hallo DSVM:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Laten we vereenvoudigen Hallo model toomake deze demonstratie eenvoudiger tooimplement. Kies Hallo drie variabelen in Hallo besluit dichtstbijzijnde toohello hoofddomeinstructuur en bouwen van een nieuwe boomstructuur met behulp van alleen die drie variabelen:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Moet een voorspellingsfunctie waarmee Hallo functies als invoer en retourneert Hallo voorspelde waarden:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Hallo predictSpam functie tooAzureML met Hallo publiceren **publishWebService** functie:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Deze functie omvat Hallo **predictSpam** werkt, maakt u een webservice die met de naam **spamWebService** gedefinieerd met in- en uitgangen en retourneert informatie over nieuwe Hallo-eindpunt.

Details weergeven van Hallo gepubliceerd webservice, inclusief de API-eindpunt en toegangssleutels met Hallo-opdracht:

    spamWebService[[2]]

tootry het uit op de eerste 10 rijen van testset Hallo Hallo:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Andere hulpprogramma's gebruiken
Hallo resterende secties ziet u hoe toouse sommige Hallo-hulpprogramma's geïnstalleerd op Hallo Linux gegevens wetenschappelijke VM. Hier volgt de lijst Hallo van hulpprogramma's beschreven:

* XGBoost
* Python
* Jupyterhub
* Rammelaar
* PostgreSQL & Squirrel SQL
* SQL Server-datawarehouse

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) is een hulpprogramma waarmee een snelle en nauwkeurige gestimuleerd structuur-implementatie.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost kunnen ook aanroepen vanuit python of een opdrachtregel.

## <a name="python"></a>Python
Voor de ontwikkeling met behulp van Python, zijn distributies van Hallo Anaconda Python 2.7 en 3.5 geïnstalleerd in Hallo DSVM.

> [!NOTE]
> Hallo Anaconda distributie omvat [Condas](http://conda.pydata.org/docs/index.html), die mag gebruikte toocreate aangepaste omgevingen voor Python die verschillende versies en/of de pakketten die in deze geïnstalleerd.
>
>

We lezen in een aantal Hallo spambase gegevensset en Hallo e-mailberichten classificeren met ondersteuning voor virtuele machines vector in scikit-informatie:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake voorspellingen:

    clf.predict(X.ix[0:20, :])

tooshow hoe toopublish een eindpunt voor met AzureML, gaan we maken een eenvoudigere model Hallo drie variabelen als toen we Hallo R model eerder hebt gepubliceerd.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish hello model tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> Dit is alleen beschikbaar voor python 2.7 en nog niet wordt ondersteund op 3.5. Voer met **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub
Hallo Anaconda distributie in Hallo DSVM wordt geleverd met een Jupyter-notebook, een omgeving met meerdere platforms tooshare Python, R of Julia code en analyse. Hallo Jupyter-notebook toegankelijk is via JupyterHub. U zich aanmelden met uw lokale Linux-gebruikersnaam en wachtwoord op ***https://\<VM DNS-naam of IP-adres\>: 8000 /***. Alle configuratiebestanden voor JupyterHub zijn gevonden in map **/etc/jupyterhub**.

Verschillende voorbeeldquery notitieblokken zijn al geïnstalleerd op Hallo VM:

* Zie Hallo [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) voor een voorbeeld Python-notebook.
* Zie [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) voor een voorbeeld van een **R** notebook.
* Zie Hallo [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) voor een ander voorbeeld **Python** notebook.

> [!NOTE]
> Hallo Julia taal is ook beschikbaar via de opdrachtregel Hallo op Hallo Linux gegevens wetenschappelijke VM.
>
>

## <a name="rattle"></a>Rammelaar
[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R analytische hulpprogramma tooLearn eenvoudig hello) is een grafisch hulpprogramma R voor gegevensanalyse. Heeft een intuïtieve interface waarmee u eenvoudig tooload kunt, verkennen, en gegevens transformeren en bouwen en evalueren van modellen.  Hallo artikel [Rattle: A Data Mining GUI voor R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) biedt een overzicht over de functies.

Installeren en start Rammelaar Hello volgende opdrachten:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> De installatie is niet vereist op Hallo DSVM. Maar Rammelaar wordt u mogelijk gevraagd extra pakketten tooinstall wanneer deze wordt geladen.
>
>

Rammelaar maakt gebruik van een tabblad-gebaseerde interface. De meeste Hallo tabbladen overeenkomen toosteps in Hallo [gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), zoals het laden van gegevens of het verkennen. Hallo gegevens wetenschap proces loopt van links tooright via Hallo tabbladen. Maar Hallo laatste tabblad bevat een logboek van Hallo R-opdrachten door Rammelaar worden uitgevoerd.

tooload en Hallo gegevensset configureren:

* tooload Hallo-bestand, selecteer Hallo **gegevens** tabblad vervolgens
* Kies Hallo selector volgende te**Filename** en kies **spambaseHeaders.data**.
* tooload Hallo-bestand. Selecteer **Execute** in Hallo bovenste rij knoppen. U ziet een overzicht van elke kolom, met inbegrip van het geïdentificeerde gegevenstype, of u nu invoer, een doel of andere type variabele en het aantal unieke waarden Hallo.
* Rammelaar geconstateerd correct Hallo **spam** kolom als Hallo doel. Selecteer Hallo spam kolom en vervolgens set Hallo **gegevens doeltype** te**Categoric**.

tooexplore hello gegevens:

* Selecteer Hallo **verkennen** tabblad.
* Klik op **samenvatting**, klikt u vervolgens **Execute**, toosee enige informatie over de typen Hallo-variabelen en sommige samenvattende statistieken.
* tooview andere soorten statistieken over elke variabele, selecteer andere opties zoals **Beschrijf** of **basisbeginselen**.

Hallo **verkennen** tabblad kunt u ook toogenerate veel begrijpelijke manier mee worden uitgezet. een histogram van Hallo gegevens tooplot:

* Selecteer **distributies**.
* Controleer **Histogram** voor **word_freq_remove** en **word_freq_you**.
* Selecteer **uitvoeren**. U ziet dat beide dichtheid worden uitgezet in een grafiekvenster van één wanneer het duidelijk is dat Hallo woord "u" vaker wordt weergegeven in e-mailberichten dan 'verwijderen'.

Er zijn ook Hallo correlatie waarnemingspunten interessante. toocreate een:

* Kies **correlatie** als Hallo **Type**, klikt u vervolgens
* Selecteer **uitvoeren**.
* Rammelaar waarschuwt u raadt maximaal 40 variabelen. Selecteer **Ja** tooview Hallo tekent.

Er zijn enkele interessante correlaties die afkomstig van zijn: 'technologie' sterk te worden gecorreleerd 'HP' en 'labs' voor het voorbeeld. Dit wordt ook sterk gecorreleerd te '650', omdat het netnummer Hallo van Hallo gegevensset donors 650.

Hallo numerieke waarden voor Hallo correlaties tussen woorden zijn beschikbaar in Hallo verkennen venster. Het is interessant toonote, bijvoorbeeld 'technologie' op de negatieve worden gecorreleerd met "uw" en 'geld'.

Rammelaar kunt Hallo gegevensset toohandle transformeren enkele veelvoorkomende problemen. Bijvoorbeeld, u kunt functies toorescale, rekenen ontbrekende waarden, uitschieters verwerken en variabelen of opmerkingen met ontbrekende gegevens verwijderen. Rammelaar kunt ook regels van de koppeling tussen opmerkingen en/of variabelen identificeren. Deze tabbladen zijn buiten het bereik van deze Introductie.

Rammelaar kunt ook cluster analyse uitvoeren. Laten we enkele functies toomake Hallo uitvoer eenvoudiger tooread uitsluiten. Op Hallo **gegevens** Kies **negeren** volgende tooeach van Hallo variabelen behalve deze tien items:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* ongewenste e-mail

Vervolgens gaat u terug toohello **Cluster** Kies **KMeans**, en set Hallo *aantal clusters* too4. Vervolgens **uitvoeren**. Hallo resultaten worden weergegeven in het uitvoervenster Hallo. Een cluster met hoge frequentie van 'george' en 'hp' heeft en is waarschijnlijk een legitieme zakelijke-e-mailadres.

een eenvoudige decision tree machine learning-model toobuild:

* Selecteer Hallo **Model** tabblad
* Kies **structuur** als Hallo **Type**.
* Selecteer **Execute** toodisplay Hallo structuur in tekstvorm in Hallo venster uitvoer.
* Selecteer Hallo **tekenen** knop tooview een grafische versie. Dit lijkt vergelijkbaar toohello structuur we verkregen eerder met behulp van *rpart*.

Een van de Hallo nice functies van Rammelaar is de mogelijkheid toorun enkele machine learning-methoden en ze snel te evalueren. Hier volgt Hallo procedure:

* Kies **alle** voor Hallo **Type**.
* Selecteer **uitvoeren**.
* Na voltooiing klikt u op enkel **Type**, bijvoorbeeld **SVM**, en Hallo resultaten te bekijken.
* U kunt ook Hallo prestaties van modellen op Hallo validatie ingesteld met Hallo Hallo vergelijken **Evaluate** tabblad. Bijvoorbeeld, Hallo **fout Matrix** selectie ziet u Hallo verwarring matrix, algemene fout en gemiddelde klasse fout voor elk model op Hallo validatie set.
* U kunt ook tekenen ROC-curve, analyse van de gevoeligheid en andere soorten model evaluaties doen.

Wanneer u klaar bent voor het bouwen van modellen, selecteren Hallo **logboek** tabblad tooview Hallo R code uitvoeren met Rammelaar tijdens uw sessie. U kunt selecteren Hallo **exporteren** knop toosave deze.

> [!NOTE]
> Er is een fout in de huidige release van Rammelaar. toomodify Hallo script of gebruik het toorepeat stappen van de hoger, moet u een teken # vóór * exporteren... dit logboek * in de tekst hello van Hallo logboek.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL & Squirrel SQL
Hallo DSVM wordt geleverd met PostgreSQL geïnstalleerd. PostgreSQL is een geavanceerde, open-source relationele database. Deze sectie wordt beschreven hoe tooload onze gegevensset in PostgreSQL spam en deze vervolgens een query.

Voordat u Hallo gegevens laden kunt, moet u tooallow wachtwoordverificatie van Hallo localhost. Bij een opdrachtprompt:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Aan de onderkant Hallo van configuratiebestand Hallo zijn verschillende regels die in details Hallo verbindingen toegestaan:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Wijzig Hallo 'IPv4 lokale verbindingen' regel toouse md5 in plaats van ident, zodat we kunt aanmelden met een gebruikersnaam en wachtwoord:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

En Hallo postgres service opnieuw starten:

    sudo systemctl restart postgresql

toolaunch psql, een interactief terminal voor PostgreSQL als gebruiker met ingebouwde postgres Hallo Voer Hallo volgende opdracht vanaf een opdrachtprompt:

    sudo -u postgres psql

Een nieuw gebruikersaccount maken, met behulp van dezelfde gebruikersnaam Hallo als u momenteel bent aangemeld als account voor Linux Hallo en wijs hieraan een wachtwoord:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Meld u vervolgens in toopsql als uw gebruikers:

    psql

En Hallo gegevens importeren in een nieuwe database:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Nu gaan we Hallo gegevens verkennen en uitvoeren van sommige query's met behulp van **Squirrel SQL**, een grafisch hulpprogramma waarmee u communiceren met databases via een JDBC-stuurprogramma.

tooget gestart, start SQL Squirrel in Hallo toepassingen menu. tooset van Hallo stuurprogramma:

* Selecteer **Windows**, klikt u vervolgens **stuurprogramma's weergeven**.
* Met de rechtermuisknop op **PostgreSQL** en selecteer **stuurprogramma wijzigen**.
* Selecteer **Extra klasse pad**, klikt u vervolgens **toevoegen**.
* Voer ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** voor Hallo **bestandsnaam** en
* Selecteer **Open**.
* Lijst met stuurprogramma's kiezen en selecteer vervolgens **org.postgresql.Driver** in **klassenaam**, en selecteer **OK**.

tooset hello verbinding toohello lokale server:

* Selecteer **Windows**, klikt u vervolgens **aliassen weergeven.**
* Kies Hallo  **+**  toomake knop een nieuwe alias.
* Naam *Spam database*, kies **PostgreSQL** in Hallo **stuurprogramma** vervolgkeuzelijst.
* Hallo-URL te instellen*jdbc:postgresql://localhost/spam*.
* Voer uw *gebruikersnaam* en *wachtwoord*.
* Klik op **OK**.
* Hallo tooopen **verbinding** venster, dubbelklikt u op Hallo ***Spam database*** alias.
* Selecteer **Verbinden**.

toorun sommige query's:

* Selecteer Hallo **SQL** tabblad.
* Voer een eenvoudige query zoals `SELECT * from data;` in Hallo query tekstvak bovenaan Hallo Hallo SQL tabblad.
* Druk op **Ctrl + Enter** toorun deze. Standaard Squirrel SQL Hallo eerste 100 rijen geretourneerd uit uw query.

Er zijn veel meer query's die u tooexplore deze gegevens kunt uitvoeren. Hoe werkt bijvoorbeeld Hallo frequentie van Hallo word *maken* verschillen tussen spam en ham?

    SELECT avg(word_freq_make), spam from data group by spam;

Of wat Hallo kenmerken van e-mailbericht dat vaak bevatten *3d*?

    SELECT * from data order by word_freq_3d desc;

De meeste e-mailberichten waarvoor een hoge exemplaar van *3d* zijn blijkbaar spam, zodat het mogelijk een handige functie voor het bouwen van een Voorspellend model tooclassify Hallo e-mailberichten.

Indien u tooperform machine learning met gegevens die zijn opgeslagen in een PostgreSQL-database wenste, kunt u overwegen [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>SQL Server-datawarehouse
Azure SQL Data Warehouse is een schaalbare clouddatabase die geschikt is voor het verwerken van grote hoeveelheden relationele en/of niet-relationele gegevens. Zie voor meer informatie [wat is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello datawarehouse op en Hallo tabel maken uitvoeren Hallo volgende opdracht uit vanaf een opdrachtprompt:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

Klik op Hallo sqlcmd-opdrachtprompt:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Gegevens kopiëren met bcp:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> Hallo regeleinden in het gedownloade bestand Hallo zijn Windows-stijl, maar bcp verwacht UNIX-stijl, dus we er tootell bcp dat met moeten - r-vlag Hallo.
>
>

En de query met sqlcmd:

    select top 10 spam, char_freq_dollar from spam;
    GO

U kunt ook een query met Squirrel SQL. Uitvoeren van gelijksoortige stappen voor PostgreSQL, met behulp van Hallo Microsoft MSSQL Server JDBC-stuurprogramma, die kan worden gevonden in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Volgende stappen
Zie voor een overzicht van onderwerpen die helpt u bij het Hallo-taken die Hallo Gegevenswetenschap proces in Azure omvatten, [Team gegevens wetenschap proces](http://aka.ms/datascienceprocess).

Zie voor een beschrijving van andere scenario's voor end-to-end die laten Hallo stappen in Hallo Team gegevens wetenschappelijke processen voor specifieke scenario's zien [Team gegevens wetenschap proces scenario's](data-science-process-walkthroughs.md). Hallo-scenario's ook laten zien hoe toocombine cloud en on-premises hulpprogramma's en services in een werkstroom of pijplijn toocreate een intelligente toepassing.
