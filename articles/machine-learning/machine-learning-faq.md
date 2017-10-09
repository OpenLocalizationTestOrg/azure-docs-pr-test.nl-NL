---
title: aaaAzure Machine Learning Veelgestelde vragen (FAQ's) | Microsoft Docs
description: 'Inleiding Azure Machine Learning: veelgestelde vragen over facturering en de mogelijkheden en beperkingen van een cloudservice voor gestroomlijnde voorspellende modellen.'
keywords: inleiding machine learning,voorspellende modellen,wat is machine learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Veelgestelde vragen over Azure Machine Learning: facturering, mogelijkheden, beperkingen en ondersteuning
U vindt hier een aantal veelgestelde vragen en de bijbehorende antwoorden die betrekking hebben op Azure Machine Learning, een cloudservice voor het ontwikkelen van voorspellende modellen en operationele oplossingen via webservices. Deze Veelgestelde vragen over bieden vragen over hoe toouse Hallo-service, waaronder Hallo facturering model, mogelijkheden, beperkingen en ondersteuning.

**Hebt u een vraag die u hier niet kunt vinden?**

Azure Machine Learning heeft een forum op MSDN waar leden van Hallo gegevens wetenschappelijke community stellen over Azure Machine Learning vragen. Hello Azure Machine Learning-team bewaakt Hallo-forum. Ga toohello [Azure Machine Learning-Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch voor antwoorden of toopost een nieuwe vraag.

## <a name="general-questions"></a>Algemene vragen
**Wat is Azure Machine Learning?**

Azure Machine Learning is een volledig beheerde service die u kunt toocreate gebruiken, testen, te gebruiken en beheren van voorspellende analytische oplossingen in de cloud Hallo. Via een browser kunt u zich eenvoudig aanmelden, gegevens uploaden en direct aan de slag gaan met Machine Learning-experimenten. U kunt voorspellende modellen, een groot palet modules en een bibliotheek van sjablonen slepen en neerzetten, zodat u algemene taken snel en eenvoudig kunt uitvoeren. Zie voor meer informatie, Hallo [overzicht van de service Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/). Zie voor een inleiding toomachine learning met uitleg over de belangrijkste termen en begrippen, [inleiding tooAzure Machine Learning](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Wat is Machine Learning Studio?**

Machine Learning Studio is een workbenchomgeving waartoe u via een webbrowser toegang hebt. Machine Learning Studio biedt een palet modules in een visuele compositie-interface die u bij het maken van een end helpt-to-end-, gegevens-wetenschappelijke werkstroom in de vorm van een experiment Hallo.

Zie [Wat is Machine Learning Studio?](machine-learning-what-is-ml-studio.md) voor meer informatie over Machine Learning Studio.

**Wat is Machine Learning API-service Hallo?**

Hallo Machine Learning API-service kunt u de voorspellende modellen toodeploy zoals die zijn ingebouwd in Machine Learning Studio als schaalbare en fouttolerante webservices. Hallo-webservices die Hallo Machine Learning API-service maakt zijn REST-API's die een interface voor communicatie tussen externe toepassingen en uw predictive analytics-modellen bieden.

Zie voor meer informatie [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

**Waar worden mijn klassieke webservices weergegeven? Waar staan mijn nieuwe webservices (op basis van Azure Resource Manager)?**

Webservices die zijn gemaakt met Hallo Classic deployment model en web services, gemaakt met Hallo nieuwe Azure Resource Manager-implementatiemodel worden vermeld in Hallo [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/) portal.

Klassieke webservices worden ook vermeld [Machine Learning Studio](http://studio.azureml.net) op Hallo **webservices** tabblad.

## <a name="azure-machine-learning-questions"></a>Vragen over Azure Machine Learning
**Wat zijn Microsoft Azure Machine Learning-webservices?**

Machine Learning-webservices bieden een interface tussen een toepassing en een scoremodel voor Machine Learning-werkstromen. Een externe toepassing kunt Azure Machine Learning toocommunicate gebruiken met een Machine Learning werkstroom score-model in realtime. Een aanroep tooa Machine Learning-webservice retourneert voorspelling resultaten tooan externe toepassing. toomake een aanroep van tooa-webservice, geeft u een API-sleutel die is gemaakt tijdens de implementatie van Hallo-webservice. Een Machine Learning-webservice is gebaseerd op REST, een populaire architectuur voor webprogrammering.

Azure Machine Learning heeft twee soorten webservices:

* Aanvraag en antwoord-Service (RR's): Een lage latentie en zeer schaalbare service die een interface toohello staatloze modellen biedt gemaakt en geïmplementeerd met behulp van Machine Learning Studio.
* Batchuitvoeringsservice (BES): een asynchrone service die een batch voor gegevensrecords scoort.

Er zijn verschillende manieren tooconsume Hallo REST-API en toegang Hallo-webservice. U kunt bijvoorbeeld een toepassing in C#, R of Python schrijven met behulp van Hallo voorbeeldcode die voor u wordt gegenereerd tijdens de implementatie van Hallo-webservice.

Hallo voorbeeldcode is beschikbaar op:
- Hallo verbruiken pagina voor de webservice Hallo in hello Azure Machine Learning-webservices-portal
- Hallo API Help-pagina in Hallo web service-dashboard in Machine Learning Studio

U kunt ook Hallo voorbeeld Microsoft Excel-werkmap die voor u gemaakt en is beschikbaar in Hallo web servicedashboard in Machine Learning Studio gebruiken.

**Wat zijn Hallo belangrijkste updates tooAzure Machine Learning?**

Zie voor de meest recente updates hello, [wat is er nieuw in Azure Machine Learning](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Vragen over Machine Learning Studio
### <a name="import-and-export-data-for-machine-learning"></a>Gegevens importeren en exporteren voor Machine Learning
**Welke gegevensbronnen worden door Machine Learning ondersteund?**

U kunt gegevens tooa Machine Learning Studio-experiment op drie manieren downloaden:

- Een lokaal bestand uploaden als een gegevensset
- Een module tooimport gegevens uit cloudgegevensservices gebruiken
- Een gegevensset importeren die is opgeslagen in een ander experiment

toolearn informatie over ondersteunde bestandsindelingen, Zie [trainingsgegevens importeren in Machine Learning Studio](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>Hoe groot mag Hallo gegevensset zijn voor mijn modules?
Modules in Machine Learning Studio ondersteunen gegevenssets up too10 GB aan compacte numerieke gegevens voor algemeen gebruik. Als een module meer dan één invoer heeft, is hello 10 GB-waarde Hallo totaal van alle invoer grootte. U kunt ook een steekproef nemen uit grotere gegevenssets via query's van Hive of Azure SQL Database, of u kunt gegevens van Learning by Counts vooraf verwerken voordat u deze opneemt.  

Hallo volgende typen gegevens toolarger gegevenssets tijdens het normaliseren kunnen uitbreiden en zijn beperkt tooless dan 10 GB:

* Sparse
* Categorische gegevens
* Tekenreeksen
* Binaire gegevens

Hallo volgende modules zijn beperkt toodatasets kleiner is dan 10 GB:

* Aanbevelingsmodules
* De module Synthetic Minority Oversampling Technique (SMOTE)
* Scriptmodules: R, Python, SQL
* Modules waarbij Hallo gegevensgrootte uitvoer kunnen groter is dan invoergegevens, zoals Join- of hash-functie worden
* Kruisvalidatie, Tune Model Hyperparameters, ordinale regressie en One-vs-All-Multiklasse, wanneer het Hallo aantal herhalingen groot is

#### <a id="UploadLimit"></a>Wat zijn Hallo beperkingen voor gegevens uploaden?
Voor gegevenssets die groter dan een paar GB zijn moet het uploaden van gegevens tooAzure Storage of Azure SQL Database, of Azure HDInsight gebruiken in plaats van rechtstreeks vanuit een lokaal bestand uploaden.

**Kan ik gegevens vanaf Amazon S3 lezen?**

Als u een kleine hoeveelheid gegevens hebt en tooexpose wilt kunt deze via een HTTP-URL, dan hebt u Hallo [importgegevens] [ import-data] module. Voor grotere hoeveelheden gegevens overbrengen tooAzure opslag eerst en gebruik vervolgens Hallo [importgegevens] [ import-data] toobring module in uw experiment.
<!--

<SEE CLOUD DS PROCESS>
-->

**Is er een ingebouwde beeldregistratiefunctie?**

U kunt meer informatie over ingebouwde beeldregistratiefunctie in Hallo [afbeeldingen importeren] [ image-reader] verwijzing.

### <a name="modules"></a>Modules
**Hallo-algoritme, gegevensbron, gegevensindeling of gegevenstransformatiebewerking die ik zoek bevindt zich niet in Azure Machine Learning Studio. Wat kan ik doen?**

U kunt gaan toohello [forum met feedback van gebruikers](http://go.microsoft.com/fwlink/?LinkId=404231) toosee functie aanvragen dat we volgen. Uw stem tooa-aanvraag niet toevoegen als een functie die u zoekt is al gevraagd. Als het Hallo-functie die u zoekt niet bestaat, maakt u een nieuwe aanvraag. U kunt te Hallo status van uw aanvraag op dit forum bekijken. We houden deze lijst nauwkeurig en Hallo-status van de beschikbaarheid van functies regelmatig bijwerken. Bovendien kunt u Hallo ingebouwde ondersteuning voor R- en Python toocreate aangepaste transformaties wanneer deze nodig is.

**Kan ik mijn bestaande code naar Machine Learning Studio overbrengen?**

Ja, kunt u uw bestaande R- of Python-code naar Machine Learning Studio uitvoeren in Hallo dezelfde experimenteren met Azure Machine Learning overbrengen en Hallo oplossing implementeren als een webservice via Azure Machine Learning overbrengen. Zie [Uw experiment uitbreiden met R](machine-learning-extend-your-experiment-with-r.md) en [Python machine learning-scripts in Azure Machine Learning Studio uitvoeren](machine-learning-execute-python-scripts.md) voor meer informatie.

**Is het mogelijk toouse als [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine een model?**

Nee, Predictive Model Markup Language (PMML) wordt niet ondersteund. U kunt aangepaste R en Python code toodefine een module.

**Hoeveel modules kan ik parallel uitvoeren in mijn experiment?**  

U kunt de up toofour modules parallel in een experiment uitvoeren.

### <a name="data-processing"></a>Gegevensverwerking
**Is er een toovisualize gegevens mogelijkheid binnen Hallo experiment interactief (anders dan R-visualisatie)?**

Klik op Hallo-uitvoer van een module toovisualize Hallo gegevens en statistieken opvragen.

**Wanneer een voorbeeldweergave resultaten of gegevens in een browser, is Hallo aantal rijen en kolommen beperkt. Waarom is dat?**

Omdat grote hoeveelheden gegevens mogelijk tooa browser worden verzonden, is het gegevensgrootte beperkt tooprevent Machine Learning Studio wordt vertraagd. toovisualize alle Hallo/resultaten, van betere toodownload Hallo van gegevens en gebruiken van Excel of een ander hulpprogramma.

### <a name="algorithms"></a>Algoritmen
**Welke bestaande algoritmen worden ondersteund in Machine Learning Studio?**

Machine Learning Studio biedt geavanceerde algoritmen, zoals schaalbare beslissingsstructuren, Bayesiaanse aanbevelingssystemen, Deep Neural Networks en Decision Jungles die zijn ontwikkeld door Microsoft Research. Ook bevat het schaalbare open-source machine learning-pakketten, zoals Vowpal Wabbit. Machine Learning Studio ondersteunt machine learning-algoritmen voor multiklassen en binaire classificatie, regressie en clusters. Hallo volledige lijst met [Machine Learning-Modules][machine-learning-modules].

**U automatisch Hallo juiste Machine Learning-algoritme toouse voor mijn gegevens voorgesteld?**

Nee, maar Machine Learning Studio heeft verschillende manieren toocompare Hallo resultaten van elk algoritme toodetermine Hallo juiste is voor uw probleem.

**Hebt u richtlijnen voor het verzamelen van één algoritme op een andere voor Hallo opgegeven algoritmen?**

Zie [hoe toochoose een algoritme](machine-learning-algorithm-choice.md).

**Hallo opgegeven algoritmen in zijn geschreven R- of Python?**

Nee, worden deze algoritmen voornamelijk in gecompileerde talen tooprovide betere prestaties geschreven.

**Worden er details van Hallo geleverde algoritmen gegeven?**

Hallo documentatie biedt informatie over Hallo algoritmen en parameters voor het afstemmen zijn beschreven toooptimize Hallo algoritme voor het gebruik.  

**Is er ondersteuning voor een onlinecursus?**

Nee, momenteel wordt alleen programmatisch opnieuw trainen ondersteund.

**Kan ik Hallo lagen van een Neural Net-Model visualiseren met behulp van de ingebouwde module Hallo?**

Nee.

**Kan ik mijn eigen modules in C# of een andere taal maken?**

U kunt op dit moment alleen R toocreate nieuwe aangepaste modules gebruiken.

### <a name="r-module"></a>R-module
**Welke R-pakketten zijn beschikbaar in Machine Learning Studio?**

Machine Learning Studio ondersteunt meer dan 400 CRAN R-vandaag pakketten en hier is Hallo [huidige lijst](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) opgenomen van alle pakketten. Zie ook [uw experiment uitbreiden met R](machine-learning-extend-your-experiment-with-r.md) toolearn hoe tooretrieve deze lijst zelf. Als Hallo-pakket dat u wilt dat zich niet in deze lijst, geeft u Hallo-naam van het Hallo-pakket op Hallo [forum met feedback van gebruikers](http://go.microsoft.com/fwlink/?LinkId=404231).

**Is het mogelijk toobuild een aangepaste R-module?**

Ja, zie [Aangepaste R-modules in Azure Machine Learning maken](machine-learning-custom-r-modules.md) voor meer informatie.

**Is er een REPL-omgeving voor R?**

Nee, is er geen lees-Eval-Print-lus (REPL)-omgeving voor R in Hallo studio.

### <a name="python-module"></a>Python-module
**Is het mogelijk toobuild een aangepaste Python-module?**

Momenteel niet, maar u kunt een of meer [Python Script uitvoeren] [ python] modules tooget Hallo hetzelfde resultaat.

**Is er een REPL-omgeving voor Python?**

U kunt Hallo Jupyter Notebooks in Machine Learning Studio gebruiken. Zie [Jupyter Notebooks introduceren in Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx) voor meer informatie.

## <a name="web-service"></a>Webservice
### <a name="retrain"></a>Retrain
**Hoe kan ik Retrain programmatisch uitvoeren voor Azure Machine Learning-modellen?**

Hallo retraining API's gebruiken. Zie [Machine Learning-modellen programmatisch opnieuw trainen](machine-learning-retrain-models-programmatically.md) voor meer informatie. Voorbeeldcode is ook beschikbaar in Hallo [Microsoft Azure Machine Learning Retraining-Demo](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Maken
**Kan ik Hallo model lokaal of in een toepassing die niet over een internetverbinding beschikken implementeren?**

Nee.

**Is er een standaardwachttijd voor alle webservices?**

Zie Hallo [Azure-abonnement limieten](../azure-subscription-service-limits.md).

### <a name="use"></a>Gebruiken
**Wanneer ik wilt toorun mijn voorspellende model als een batchuitvoeringsservice en een Request Response-service?**

Hallo Request Response-service (RR's) is een lage latentie en hoge schaalbaarheid webservice die is gebruikt tooprovide een interface toostateless modellen die zijn gemaakt en geïmplementeerd vanuit Hallo experimentele omgeving. Hallo batchuitvoeringsservice (BES) is een service die asynchroon scores een batch gegevensrecords. Hallo invoer voor BES is zoals gegevensinvoer die gebruikmaakt van Bronrecords. Hallo belangrijkste verschil is dat BES een blok records uit diverse bronnen, zoals Azure Blob storage, Azure Table storage, Azure SQL Database, HDInsight (hive query) en HTTP-bronnen leest. Zie voor meer informatie [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

**Hoe kan ik Hallo-model voor Hallo geïmplementeerde webservice bijwerken?**

tooupdate een Voorspellend model voor een reeds geïmplementeerde service wijzigen en Hallo experiment dat u tooauthor gebruikt opnieuw uitvoeren en Hallo getraind model opslaan. Nadat u een nieuwe versie van Hallo getrainde model beschikbaar hebt, Machine Learning Studio wordt u gevraagd als u wilt dat tooupdate uw webservice. Voor meer informatie over hoe u een geïmplementeerde webservice tooupdate Zie [een Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

U kunt ook Hallo Retraining API's gebruiken.
Zie [Machine Learning-modellen programmatisch opnieuw trainen](machine-learning-retrain-models-programmatically.md) voor meer informatie. Voorbeeldcode is ook beschikbaar in Hallo [Microsoft Azure Machine Learning Retraining-Demo](https://azuremlretrain.codeplex.com/).

**Hoe bewaak ik mijn geïmplementeerde webservice in productie?**

Nadat u een Voorspellend model hebt geïmplementeerd, kunt u het bewaken van Hallo klassieke Azure portal (alleen voor klassieke webservices) of hello Azure Machine Learning-webservices-portal. Elke geïmplementeerde service heeft een eigen dashboard met de controlegegevens voor de service. Voor meer informatie over hoe toomanage uw geïmplementeerde web-services, Zie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md) en [beheren van een Azure Machine Learning-werkruimte](machine-learning-manage-workspace.md).

**Is er een plaats waar kan ik Hallo-uitvoer van mijn RRS/BES zien?**

Voor RRS is is Hallo web service-antwoord meestal waar u Hallo resultaten bekijken. U kunt dit ook schrijven tooAzure Blob-opslag. Voor BES kunnen Hallo-uitvoer standaard tooa blob geschreven. U kunt ook Hallo uitvoer tooa database of tabel schrijven met behulp van Hallo [gegevens exporteren] [ export-data] module.

**Kan ik alleen webservices maken van modellen die in Machine Learning Studio zijn gemaakt?**

Nee, u kunt ook webservices rechtstreeks met behulp van Jupyter Notebooks en RStudio maken.

**Waar vind ik informatie over foutcodes?**

Zie [Machine Learning Module-foutcodes](https://msdn.microsoft.com/library/azure/dn905910.aspx) voor een lijst met foutcodes en beschrijvingen.

## <a name="scalability"></a>Schaalbaarheid
**Wat is de schaalbaarheid van de webservice Hallo Hallo?**

Hallo standaardeindpunt is momenteel voorzien van 20 gelijktijdige RRS-aanvragen per eindpunt. U kunt deze too200 gelijktijdige aanvragen per eindpunt schalen en u kunt elke web service too10, 000 eindpunten per webservice schalen zoals beschreven in [schalen van een webservice](machine-learning-scaling-webservice.md). Voor BES kunnen op elk eindpunt 40 aanvragen tegelijk worden verwerkt; extra aanvragen worden in de wachtrij geplaatst. Aanvragen in de wachtrij automatisch worden uitgevoerd als Hallo wachtrij afneemt.

**Worden R-taken verdeeld over knooppunten?**

Nee.  

**Hoeveel gegevens kan ik gebruiken voor training?**

Modules in Machine Learning Studio ondersteunen gegevenssets up too10 GB aan compacte numerieke gegevens voor algemeen gebruik. Als een module meer dan één invoer, Hallo totaal is de grootte voor alle invoer 10 GB. U kunt ook een steekproef nemen uit grotere gegevenssets via Hive-query's, Azure SQL Database-query's, of gegevens uit [Learning with Counts][counts]-modules vooraf verwerken voordat u deze opneemt.  

Hallo volgende typen gegevens toolarger gegevenssets tijdens het normaliseren kunnen uitbreiden en zijn beperkt tooless dan 10 GB:

* Sparse
* Categorische gegevens
* Tekenreeksen
* Binaire gegevens

Hallo volgende modules zijn beperkt toodatasets kleiner is dan 10 GB:

* Aanbevelingsmodules
* De module Synthetic Minority Oversampling Technique (SMOTE)
* Scriptmodules: R, Python, SQL
* Modules waarbij Hallo gegevensgrootte uitvoer kunnen groter is dan invoergegevens, zoals Join- of hash-functie worden
* Kruisvalidatie, Tune Model Hyperparameters, ordinale regressie en One-vs-All-multiklasse, wanneer het aantal herhalingen groot is

Voor gegevenssets die groter dan een paar GB zijn moet het uploaden van gegevens tooAzure Storage of Azure SQL Database of HDInsight gebruiken in plaats van rechtstreeks vanuit een lokaal bestand uploaden.

**Zijn er beperkingen voor de vectorgrootte?**

Rijen en kolommen zijn elke beperkt toohello .NET-beperking van Max Int: 2.147.483.647.

**Kan ik aanpassen Hallo grootte van Hallo virtuele machine die wordt uitgevoerd Hallo webservice?**

Nee.  

## <a name="security-and-availability"></a>Beveiliging en beschikbaarheid
**Standaard die toegang tot http-eindpunt voor de webservice Hallo Hallo? Hoe beperk ik toegang toohello eindpunt**

Na de implementatie van een webservice wordt een standaardeindpunt voor de service gemaakt. Hallo standaardeindpunt kan worden aangeroepen met behulp van de API-sleutel. U kunt toevoegen om dat meer eindpunten met hun eigen sleutels van Hallo klassieke Azure-portal of programmatisch met behulp van Hallo Web Service Management-API's. Toegangstoetsen zijn benodigde toomake oproepen toohello-webservice. Zie voor meer informatie [hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

**Wat gebeurt er als mijn Azure-opslagaccount niet kan worden gevonden?**

Machine Learning Studio is afhankelijk van een gebruiker opgegeven Azure storage-account toosave tussenliggende gegevens wanneer het Hallo-werkstroom wordt uitgevoerd. Dit opslagaccount weergegeven tooMachine Learning Studio wanneer een werkruimte wordt gemaakt. Na het Hallo werkruimte gemaakt als Hallo storage-account wordt verwijderd en kan niet meer worden gevonden, Hallo werkruimte functioneert en alle experimenten in deze werkruimte mislukken.

Als u per ongeluk Hallo storage-account verwijderd, opnieuw Hallo storage-account met dezelfde naam in Hallo Hallo dezelfde regio bevinden als Hallo verwijderd opslagaccount. Daarna resync Hallo toegangssleutel.

**Wat gebeurt er als mijn toegangssleutel voor het opslagaccount niet meer is gesynchroniseerd?**

Machine Learning Studio is afhankelijk van een gebruiker opgegeven Azure storage-account toostore tussenliggende gegevens wanneer het Hallo-werkstroom wordt uitgevoerd. Dit opslagaccount weergegeven tooMachine Learning Studio wanneer een werkruimte wordt gemaakt en Hallo toegangstoetsen gekoppeld aan deze werkruimte zijn. Als Hallo toegangstoetsen zijn gewijzigd nadat het Hallo-werkruimte is gemaakt, toegang Hallo werkruimte geen meer Hallo storage-account. De werkruimte functioneert niet meer en alle experimenten in deze werkruimte mislukken.

Als u de toegangssleutels voor opslag-account hebt gewijzigd, Hallo resync Hallo toegangstoetsen in de werkruimte Hallo met behulp van de klassieke Azure-portal.  

## <a name="support-and-training"></a>Ondersteuning en training
**Waar kan ik training krijgen voor Azure Machine Learning?**

Hallo [Azure Machine Learning-documentatiecentrum](https://azure.microsoft.com/services/machine-learning/) video's voor zelfstudies en hoe tooguides host. Deze stapsgewijze instructies Hallo diensten en Hallo gegevens wetenschappelijke levenscyclus van het importeren van gegevens, opruimen van gegevens, ontwikkelen van voorspellende modellen en in productie implementeert met behulp van Azure Machine Learning toegelicht.

We toevoegen nieuwe wezenlijke toohello Machine Learning Center voortdurend. U kunt aanvragen versturen voor extra materiaal in Machine Learning Center op Hallo [forum met feedback van gebruikers](https://windowsazure.uservoice.com/forums/257792-machine-learning).

U vindt ook trainingsmateriaal op [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**Waar kan ik ondersteuning krijgen voor Azure Machine Learning?**

technische ondersteuning voor Azure Machine Learning tooget te gaan[ondersteuning van Azure](/support/options/), en selecteer **Machine Learning**.

Azure Machine Learning heeft ook een communityforum op MSDN waar u vragen kunt stellen over Azure Machine Learning. Hello Azure Machine Learning-team bewaakt Hallo-forum. Ga te[Azure-Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Vragen over facturering
**Hoe werkt de facturering in Machine Learning?**

Azure Machine Learning bestaat uit twee onderdelen: Machine Learning Studio en Machine Learning-webservices.

Terwijl u evaluatie van Machine Learning Studio, kunt u gratis facturering laag Hallo. Hallo gratis laag kunt u ook een klassiek webservice met capaciteit beperkte implementeren.

Als u besluit dat Azure Machine Learning aan uw behoeften voldoet, kunt u zich registreert voor Hallo Standard-laag. toosign up, moet u een Microsoft Azure-abonnement hebben.

In de standaardcategorie hello, wordt u maandelijks gefactureerd voor elke werkruimte die u in Machine Learning Studio definieert. Wanneer u een experiment in Hallo studio uitvoert, wordt u gefactureerd voor rekenresources wanneer u een experiment worden uitgevoerd. Als u een webservice klassiek, transacties implementeert en compute uur worden gefactureerd op basis van Hallo omslagstelsel.

Nieuwe (op Resource Manager gebaseerde) webservices introduceren abonnementen waarmee de kosten beter te voorspellen zijn. Prijzen voor gelaagde biedt kortingen toocustomers die een grote hoeveelheid capaciteit nodig hebben.

Wanneer u een plan maakt, doorvoeren tooa vaste kosten die wordt geleverd met een inbegrepen aantal API-rekenuren en API-transacties. Als u meer opgenomen hoeveelheden nodig hebt, kunt u exemplaren tooyour abonnement kunt toevoegen. Als u veel meer inbegrepen hoeveelheden nodig hebt, kunt u een plan uit een van de hogere lagen kiezen met meer inbegrepen hoeveelheden en een beter kortingstarief.

Nadat hello opgenomen hoeveelheden in bestaande exemplaren worden gebruikt, als u meer informatie over het gebruik is in rekening gebracht met Hallo overschrijding frequentie die is gekoppeld aan Hallo facturering plan laag.

> [!NOTE]
Opgenomen hoeveelheden opnieuw zijn toegewezen voor elke 30 dagen en ongebruikte opgenomen hoeveelheden kunnen niet overschakelen toohello met de volgende periode.

Zie [Machine Learning-prijzen](https://azure.microsoft.com/pricing/details/machine-learning/) voor aanvullende informatie over de facturering en prijzen.

**Is er een gratis proefversie van Machine Learning?**

 Voor Azure Machine Learning bestaat de mogelijkheid om voor een gratis abonnement te kiezen. Dit wordt uitgelegd in [Prijzen van Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/). Machine Learning Studio beschikt over een proefversie van acht uur snelle evaluatie die beschikbaar is wanneer u zich aanmeldt te[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).

 Als u zich registreert voor een gratis proefversie van Azure, kunt u bovendien alle Azure-services een maand proberen. toolearn meer informatie over Hallo gratis proefversie van Azure, gaat u naar [gratis proefabonnement Veelgestelde vragen over Azure](https://azure.microsoft.com/pricing/free-trial-faq/).

**Wat is een transactie?**

Een transactie vertegenwoordigt een API-aanroep waarop Azure Machine Learning reageert. Transacties van de Request-Response-service (RRS) en aanroepen van de batchuitvoeringsservice (BES) worden bij elkaar opgeteld en verrekend met uw abonnement.

**Kan ik Hallo opgenomen transactie hoeveelheden gebruiken in een plan voor RRS- en BES?**

Ja, de RRS- en BES-transacties worden bij elkaar opgeteld en verrekend met uw abonnement.

**Wat is een API-rekenuur?**

Een API compute uur is Hallo facturering eenheid voor API-aanroepen nemen toorun met behulp van Machine Learning rekenresources Hallo-tijd. Al uw aanroepen worden bij elkaar opgeteld voor factureringsdoeleinden.

**Hoe lang duurt een productie-API-aanroep gewoonlijk?**

Productie-API-aanroep keren kunnen aanzienlijk variëren doorgaans variërend van honderden milliseconden tooa enkele seconden. Sommige API-aanroepen mogelijk minuten, afhankelijk van de complexiteit Hallo van Hallo gegevensverwerking en machine learning-model. Hallo aanbevolen manier tooestimate productie-API-aanroep keren toobenchmark een model op Hallo Machine Learning-service is.

**Wat is een Studio-rekenuur?**

Een compute Studio uur is Hallo facturering eenheid voor Hallo cumulatieve tijd dat uw experimenten rekenresources in studio gebruiken.

**In de (nieuwe Azure Resource Manager gebaseerde) webservices, wat Hallo ontwikkelen en testen laag zijn alleen bedoeld voor?**

Resource Manager gebaseerde webservices bieden meerdere lagen die u tooprovision uw abonnement gebruiken kunt. Hallo biedt ontwikkelen en testen prijscategorie beperkte, opgenomen hoeveelheden waarmee u tootest uw experiment als een webservice zonder kosten. U hebt Hallo kans toosee hoe het werkt.

**Zijn er afzonderlijke opslagkosten?**

Machine Learning gratis laag Hallo geen vereist of afzonderlijke opslag toestaan. Hallo Machine Learning standaardcategorie vereist gebruikers toohave Azure storage-account. Azure Storage wordt [afzonderlijk gefactureerd](https://azure.microsoft.com/pricing/details/storage/).

**Ondersteunt Machine Learning hoge beschikbaarheid?**

Ja. Zie voor meer informatie [Machine Learning-prijzen](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) voor een beschrijving van Hallo serviceovereenkomst (SLA).

**Met welk specifiek type rekenresources worden mijn productie-API-aanroepen uitgevoerd?**

Hallo Machine Learning-service is een multitenant-service. Werkelijke rekenresources die worden gebruikt op de back-end Hallo variëren en zijn geoptimaliseerd voor prestaties en hoge voorspelbaarheid is vereist.

### <a name="management-of-new-resource-manager-based-web-services"></a>Beheer van nieuwe (op Resource Manager gebaseerde) webservices
**Wat gebeurt er als ik mijn plan verwijder?**

Hallo-abonnement is verwijderd uit uw abonnement en u wordt gefactureerd voor gebruik naar rato.

> [!NOTE]
Een plan dat door een webservice wordt gebruikt, kan niet worden verwijderd. toodelete hello plan, moet u ofwel toewijzen een nieuwe webservice toohello plannen of Hallo-webservice verwijderen.

**Wat is een planexemplaar?**

Een exemplaar van de planning is een eenheid van de opgenomen hoeveelheden dat u tooyour Facturering abonnement kunt toevoegen. Als u een factureringscategorie voor uw abonnement selecteert, heeft deze één exemplaar. Als u meer opgenomen hoeveelheden nodig hebt, kunt u exemplaren van Hallo geselecteerde laag tooyour abonnement kunt toevoegen.

**Hoeveel planexemplaren kan ik toevoegen?**

U kunt één exemplaar van de prijscategorie van Hallo ontwikkelen en testen in een abonnement hebben.

Voor de lagen Standard S1, Standard S2 en Standard S3 kunt u er net zoveel toevoegen als u wilt.

> [!NOTE]
Afhankelijk van het verwachte gebruik deze mogelijk worden rendabeler tooupgrade tooa laag die hoeveelheden meer opgenomen in plaats exemplaren toohello huidige laag toevoegen.

**Wat gebeurt er als ik planlagen wijzig (een upgrade/downgrade uitvoer)?**

Hallo oude plan is verwijderd en het huidige gebruik hello wordt gefactureerd op basis van naar rato. Een nieuw plan met Hallo volledige opgenomen hoeveelheden Hallo bijgewerkt/Downgrade uitgevoerd voor de laag wordt gemaakt voor de rest van de periode Hallo Hallo.

> [!NOTE]
Inbegrepen hoeveelheden worden per periode toegewezen en ongebruikte hoeveelheden kunnen niet worden meegenomen naar de volgende periode.

**Wat gebeurt er wanneer ik Hallo exemplaren worden verhoogd met een abonnement?**

Aantallen zijn opgenomen op basis van naar rato en 24 uur toobe effectieve kunnen duren.

**Wat gebeurt er wanneer ik een planexemplaar verwijder?**

Hallo-exemplaar is verwijderd van uw abonnement en u wordt gefactureerd voor gebruik naar rato.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Aanmelden voor nieuwe (op Resource Manager gebaseerde) webservicesplannen
**Hoe registreer ik me voor een plan?**

U hebt twee manieren toocreate facturering plannen.

Wanneer u de eerste keer een nieuwe op Resource Manager gebaseerde webservice implementeert, kunt u een bestaand plan kiezen of een nieuw plan maken.

Plannen voor die u op deze manier maakt zijn in uw regio standaard en uw webservice worden geïmplementeerde toothat regio.

Als u wilt dat toodeploy services tooregions dan de regio van uw standaard, kunt u toodefine uw facturering plannen voordat u uw service implementeert.

In dat geval kunt u toohello Azure Machine Learning-webservices portal aanmelden en ga toohello plannen pagina. Hier kunt u plannen toevoegen en verwijderen, en bestaande plannen wijzigen.

**Welk schema moet ik kiezen toostart uitschakelen met?**

U wordt aangeraden dat u met de Hallo Standard-S1 begint servicetier en bewaken van uw service voor gebruik. Als u dat u van uw opgenomen hoeveelheden snel gebruikmaakt vinden, kunt u instanties toevoegen of verplaatsen tooa hogere lagen en beter kortingen krijgen. Op deze manier kunt u uw abonnement gedurende de factureringscyclus aanpassen aan uw wensen.

**Welke regio's zijn Hallo nieuwe abonnementen beschikbaar in?**

Hallo nieuwe facturering plannen zijn beschikbaar in Hallo drie regio's waar we Hallo nieuwe web-services ondersteunen:

* Zuid-centraal VS
* West-Europa
* Zuidoost-Azië

**Ik heb webservices in meerdere regio‘s. Heb ik voor elke regio een apart plan nodig?**

Ja. Planprijzen variëren per regio. Wanneer u een web service tooanother regio implementeert, moet u tooassign it een plan dat specifieke toothat regio. Zie [Producten beschikbaar per regio]( https://azure.microsoft.com/regions/services/) voor meer informatie.

### <a name="new-web-services-overages"></a>Nieuwe webservices - overschrijdingen
**Hoe kan ik controleren of mijn webserviceverbruik de limiet overschrijdt?**

U kunt Hallo gebruik op alle abonnementen op Hallo plannen pagina in hello Azure Machine Learning-webservices portal weergeven. Meld u aan toohello portal en klik vervolgens op Hallo **plannen** menuoptie.

In Hallo **transacties** en **Compute** kolommen van Hallo tabel ziet u Hallo opgenomen hoeveelheden Hallo-plan en Hallo percentage gebruikt.

**Wat gebeurt er wanneer ik gebruik up Hallo hoeveelheden in Hallo ontwikkelen en testen prijscategorie opnemen?**

Services waarvoor een ontwikkelen en testen laag toegewezen toothem prijzen zijn gestopt tot Hallo volgende periode of totdat u ze tooa betaald laag verplaatst.

**Hoe worden de prijzen voor RRS- en BES-werkbelastingen (Request Response en batches) berekend voor klassieke webservices en overschrijdingen van nieuwe (op Resource Manager gebaseerde) webservices?**

Voor een werkbelasting RRS u in rekening worden gebracht voor elke API-aanroep voor transactie die u aanbrengt en Hallo compute-tijd die is gekoppeld aan deze aanvragen. Uw transactiekosten RRS productie-API worden berekend als het totale aantal API-aanroepen die u aanbrengt Hallo vermenigvuldigd met Hallo prijs per 1.000 transacties (naar rato door afzonderlijke transactie). Uw kosten RRS API productie-API compute per uur worden berekend als hoeveelheid tijd die nodig is voor elke API-aanroep toorun, vermenigvuldigd met het totale aantal API-transacties, vermenigvuldigd met prijs per uur voor productie-API-rekenuren Hallo HALLO hallo.

Bijvoorbeeld: 1.000.000 API-transacties die elke toorun voor 0.72 seconden duren voor Standard S1 overschrijding zou leiden tot (1.000.000 * $0,50, 1K API-transacties) in $500 in productie-API-transactiekosten en (1.000.000 * 0.72 seconde * $2 / uur) $400 in productie-API-rekenuren uren voor een totaal van €900.

Voor een werkbelasting BES u in rekening worden gebracht in Hallo dezelfde manier. Echter Hallo API transactiekosten vertegenwoordigen Hallo aantal batchtaken die u verzendt en Hallo compute-kosten vertegenwoordigen Hallo compute-tijd die is gekoppeld aan deze batchtaken. Uw transactiekosten BES productie-API worden berekend als het totale aantal taken die worden verzonden hello vermenigvuldigd met Hallo prijs per 1.000 transacties (naar rato door afzonderlijke transactie). Uw kosten BES API productie-API compute per uur worden berekend als hoeveelheid tijd die nodig is voor elke rij in de taak toorun vermenigvuldigd met het totale aantal rijen in de taak vermenigvuldigd met het totale aantal taken vermenigvuldigd met Hallo prijs per productie-API Hallo HALLO hallo COMPUTE uur. Wanneer u Hallo Machine Learning Rekenmachine, gecombineerd Hallo transactie meter vertegenwoordigt Hallo aantal taken dat u van plan toosubmit bent en Hallo tijd per transactie veld Hallo vertegenwoordigt tijd die nodig is voor alle rijen in de toorun van elke taak.

Stel dat er een Standard S1-overschrijding is en dat u 100 taken per dag verzendt die elk uit 500 rijen bestaan waarvoor elk 0,72 seconden nodig zijn om ze uit te voeren. Uw maandelijkse overschrijdingskosten zijn dan (100 taken per dag = 3100 taken/mnd * $ 0,50/1K aan API-transacties) $ 1,55 aan productie-API-transactiekosten en (500 rijen * 0,72 sec * 3100 taken * $ 2/uur) $ 620 aan productie-API-rekenuren. Dit is een totaal van $ 621,55.

### <a name="azure-machine-learning-classic-web-services"></a>Microsoft Azure Machine Learning-webservices
**Is betalen per gebruik nog steeds beschikbaar?**

Ja, klassieke webservices zijn nog steeds beschikbaar in Azure Machine Learning.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Azure Machine Learning gratis laag en Standard-laag
**Wat is opgenomen in Azure Machine Learning gratis laag Hallo?**

Hello Azure Machine Learning gratis laag is beoogde tooprovide een toohello diepgaande inleiding Azure Machine Learning Studio. U hoeft een Microsoft-account toosign actief is. Hallo gratis laag omvat kaartjes tooone Azure Machine Learning Studio werkruimte per [Microsoft-account](https://www.microsoft.com/account/default.aspx). U kunt gebruiken om too10 GB aan opslagruimte en operationeel modellen als staging-API's in deze laag. Werkbelastingen uit een gratis laag worden niet gedekt door een SLA en zijn alleen bedoeld voor ontwikkeling en persoonlijk gebruik. 

Gratis laag werkruimten hebben Hallo volgende beperkingen:

* Werkbelastingen geen toegang tot gegevens door verbinding te maken tooan lokale server waarop SQL Server wordt uitgevoerd.
* U kunt geen nieuwe webservices gebaseerd op Resource Manager implementeren.


**Wat is opgenomen in hello Azure Machine Learning standaardcategorie en plannen?**

Hello Azure Machine Learning standaardcategorie is een betaald productieversie van Azure Machine Learning Studio. Hello Azure Machine Learning Studio wordt maandelijkse kosten in rekening gebracht op een per per maand per werkruimte en naar rato voor gedeeltelijke maanden. Azure Machine Learning Studio-experimenturen worden voor actieve experimenten per rekenuur gefactureerd. Facturering voor gedeeltelijke uren is naar rato.  

Hello Azure Machine Learning API-service wordt in rekening gebracht, afhankelijk van een klassiek webservice of een nieuwe (op een Resource Manager gebaseerde)-webservice.

Hallo na kosten worden per werkruimte voor uw abonnement samengevoegd.

* Abonnement voor machine Learning-werkruimte: Hallo abonnement voor Machine Learning-werkruimte is maandelijks een vast bedrag waarmee access tooa Machine Learning Studio-werkruimte. Hallo-abonnement is vereist toorun experimenten in Hallo studio en tooutilize Hallo productie-API's.
* Studio-experimenturen: alle berekeningen die moeten worden samengevoegd door experimenten in Machine Learning Studio maakt een aggregatie van deze meter en actieve productie-API-aanroepen in Hallo staging-omgeving.
* Toegang tot de gegevens door verbinding te maken tooan lokale server die SQL Server in uw modellen voor uw training uitvoert en score berekenen.
* Voor klassieke webservices:
  * Rekenuren productie-API: deze meter bevat bij elkaar opgetelde rekenkosten voor webservices die actief zijn in productie.
  * Productie-API-transacties (per 1000): deze meter bevat kosten die moeten worden samengevoegd per aanroep tooyour productie-webservice.

Naast de voorgaande kosten, in geval van Resource Manager gebaseerde webservice Hallo Hallo zijn kosten geaggregeerde toohello geselecteerde abonnement:

* Standard S2-S1/S3 API-Plan (eenheden): Deze meter Hallo type-exemplaar dat geselecteerd voor Resource Manager gebaseerde webservices vertegenwoordigt.
* Standard S2-S1-S3 overschrijding aantal API-Rekenuren: Deze meter omvat compute-kosten die moeten worden samengevoegd door Resource Manager gebaseerde web-services die worden uitgevoerd in de productieomgeving nadat de aantallen Hallo opgenomen in bestaande exemplaren is gebruikt. Hallo extra gebruik in rekening gebracht volgens Hallo overate frequentie die is gekoppeld aan S2-S1-S3 plan laag.
* Standard S2-S1/S3 overschrijding API-transacties (per 1000): deze meter bevat kosten die moeten worden samengevoegd per aanroep tooyour productie Resource Manager gebaseerde webservice na Hallo hoeveelheden opgenomen in de bestaande exemplaren zijn gebruikt. Hallo aanvullende informatie over het gebruik is in rekening gebracht volgens Hallo overate frequentie die is gekoppeld aan S2-S1-S3 plan laag.
* Inbegrepen aantal API-Rekenuren: Met Resource Manager-webservices, deze meter vertegenwoordigt aantal API-rekenuren Hallo opgenomen.
* Opgenomen hoeveelheid API-transacties (per 1000): met Resource Manager gebaseerde web-services, deze meter vertegenwoordigt Hallo opgenomen aantal API-transacties.

**Hoe registreer ik me voor de gratis laag van Azure Machine Learning?**

U hebt alleen een Microsoft-account nodig. Ga te[Azure Machine Learning-startpagina](https://azure.microsoft.com/services/machine-learning/), en klik vervolgens op **nu starten**. Meld u aan met uw Microsoft-account. Vervolgens wordt er in de gratis laag een werkruimte voor u gemaakt. U kunt starten tooexplore en Machine Learning-experimenten meteen te maken.

**Hoe registreer ik me voor de Standard-laag van Azure Machine Learning?**

U moet toegang tooan Azure-abonnement toocreate eerst een standaard Machine Learning-werkruimte hebben. U kunt zich aanmelden voor een 30 dagen gratis proefabonnement Azure-abonnement en hoger upgrade tooa betaalde Azure-abonnement of u een betaald Azure-abonnement rechtstreekse kunt aanschaffen. Vervolgens kunt u een Machine Learning-werkruimte maken vanuit de klassieke Microsoft Azure-portal Hallo nadat u toegang toohello abonnement krijgt. Weergave Hallo [Stapsgewijze instructies](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

U kunt ook worden uitgenodigd door een standaard Machine Learning werkruimte eigenaar tooaccess Hallo van eigenaar werkruimte.

**Kan ik mijn eigen toouse Azure Blob storage-account opgeven met de Hallo gratis laag**

Nee, is de standaardcategorie Hallo gelijkwaardige toohello versie Hallo Machine Learning-service is beschikbaar voordat Hallo lagen zijn geïntroduceerd.

**Kan ik mijn machine learning-modellen als API's in de gratis laag Hallo implementeren?**

Ja, u kunt operationeel machine learning-modellen toostaging API-services als onderdeel van de gratis laag Hallo. tooput Hallo staging-API-service naar de productie en ophalen van een productie-eindpunt voor Hallo geoperationaliseerd service, moet u de standaardcategorie hello gebruiken.

**Wat is Hallo verschil tussen de gratis proefversie van Azure en Azure Machine Learning gratis laag?**

Hallo [gratis proefversie van Microsoft Azure](https://azure.microsoft.com/free/) biedt-service gedurende één maand tegoeden die u tooany Azure kunt toepassen. Hello Azure Machine Learning gratis laag biedt continue toegang tot specifiek tooAzure Machine Learning voor niet-productieve werkbelastingen.

**Hoe kan ik een experiment van Hallo gratis laag toohello standaardcategorie verplaatsen?**

toocopy uw experimenten van Hallo gratis laag toohello Standard-laag:

1. Meld u aan Machine Learning Studio tooAzure en zorg ervoor dat u zowel gratis werkruimte Hallo Hallo standaard werkruimte in Hallo werkruimte selector in de bovenste navigatiebalk Hallo kunt zien.
2. Overschakelen tooFree werkruimte als u zich in de standaard Hallo-werkruimte.
3. Selecteer in de lijstweergave van Hallo experiment een experiment dat u wilt toocopy, en klik vervolgens op Hallo **kopie** opdrachtknop.
4. Selecteer standaard Hallo-werkruimte in Hallo dialoogvenster dat wordt geopend en klik vervolgens op Hallo **kopie** knop.
   Alle bijbehorende gegevenssets Hallo, getrainde model, enz., samen met de Hallo experiment standaard Hallo-werkruimte worden gekopieerd.
5. U moet toorerun Hallo experiment en publiceren van uw web-service in Hallo standaard werkruimte.

### <a name="studio-workspace"></a>Studio-werkruimte
**Krijg ik verschillende facturen voor de verschillende werkruimten?**

Kosten voor werkruimten worden voor elke toepasselijke meter afzonderlijk berekend in een enkele factuur.

**Met welk specifiek type rekenresources worden mijn experimenten uitgevoerd?**

Hallo Machine Learning-service is een multitenant-service. Werkelijke rekenresources die worden gebruikt op de back-end Hallo variëren en zijn geoptimaliseerd voor prestaties en hoge voorspelbaarheid is vereist.

### <a name="guest-access"></a>Toegang voor gasten
**Wat is de toegang voor gasten tooAzure Machine Learning Studio?**

Toegang voor gasten is een proefervaring waarvoor beperkingen gelden. U kunt in Azure Machine Learning Studio gratis en zonder verificatie experimenten maken en uitvoeren. Gast-sessies zijn niet-permanente (kan niet worden opgeslagen) en een beperkt aantal uren tooeight. Andere beperkingen zijn: geen ondersteuning voor R en Python, geen tijdelijke API's en beperkte gegevenssetgrootte en opslagcapaciteiten. Vergelijking: gebruikers die toosign met een Microsoft-account kiezen hebben volledige toegang toohello gratis laag van Machine Learning Studio dat eerder beschreven, waaronder een permanente werkruimte en uitgebreidere mogelijkheden. toochoose uw gratis Machine Learning ondervindt, klikt u op **aan de slag** op [https://studio.azureml.net](https://studio.azureml.net), en selecteer vervolgens **raden toegang** of meld u aan met een Microsoft account.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
