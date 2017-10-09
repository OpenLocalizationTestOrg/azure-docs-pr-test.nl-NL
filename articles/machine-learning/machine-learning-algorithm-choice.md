---
title: aaaHow toochoose machine learning-algoritmen | Microsoft Docs
description: Hoe toochoose Azure Machine Learning-algoritmen voor en zonder supervisie learning clustering, classificatie- of regressiemodel experimenten.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>Hoe toochoose algoritmen voor Microsoft Azure Machine Learning
Hallo toohello vraag te beantwoorden "welke machine learning-algoritme moet ik gebruiken?" is altijd "Deze afhankelijk is." Dit is afhankelijk van Hallo grootte, kwaliteit en aard van Hallo-gegevens. Deze afhankelijk is van wat u wilt toodo met Hallo antwoord. Dit is afhankelijk van hoe Hallo math van Hallo-algoritme is vertaald naar instructies voor het Hallo-computer die u gebruikt. En dit is afhankelijk van hoeveel tijd die u hebt. Zelfs Hallo meest opgetreden gegevenswetenschappers kunnen niet zien welk algoritme best zal uitvoeren voordat u ze.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Hallo cheats blad van Machine Learning-algoritme
Hallo **Microsoft Azure Machine Learning-algoritme cheats blad** helpt bij het kiezen van Hallo rechts machine learning-algoritme voor uw predictive analytics-oplossingen van Microsoft Azure Machine Learning Hallo-bibliotheek van algoritmen.
Dit artikel begeleidt u bij het toouse deze.

> [!NOTE]
> Hallo-referentieoverzicht toodownload en volg samen met dit artikel gaat te[Machine learning algorithm cheat sheet voor Microsoft Azure Machine Learning Studio](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Deze referentieoverzicht heeft een specifieke doelgroep in gedachten: een begin gegevens wetenschappelijk met undergraduate niveau machine learning, probeert toochoose een algoritme toostart met in Azure Machine Learning Studio. Dat betekent dat bepaalde generalisaties en oversimplifications maakt, maar het u in een veilige richting distributiepunten. Het betekent ook dat er veel algoritmen hier niet worden vermeld zijn. Wanneer Azure Machine Learning tooencompass een uitgebreidere set van beschikbare methoden groeit, gaan we ze toevoegen.

Deze aanbevelingen zijn gecompileerde feedback en tips van veel gegevenswetenschappers en machine learning-experts. We alles wat niet overeenkomen, maar ik heb tooharmonize onze mening geprobeerd naar een ruwe consensus. De meeste Hallo statusverklaringen geschil beginnen met "Taak afhankelijk is,..."

### <a name="how-toouse-hello-cheat-sheet"></a>Hoe toouse Hallo blad cheats
Hallo-pad en de algoritme labels op Hallo grafiek als lezen ' voor  *&lt;pad label&gt;*, gebruik  *&lt;algoritme&gt;*. " Bijvoorbeeld ' voor *snelheid*, gebruik *twee logistic regression klasse*. " Soms meer dan een vertakking is van toepassing.
Geen van hen worden soms past perfect. Ze beoogde toobe regel van de miniatuur aanbevelingen bent, dus u hoeft het exacte wordt.
Verschillende gegevenswetenschappers ik gehad met aangegeven die alleen ervoor manier om te zoeken allerbeste Hallo-algoritme is tootry Hallo ze allemaal.

Hier volgt een voorbeeld van Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) Hallo resultaten van een experiment die verschillende algoritmen tegen Hallo probeert dezelfde gegevens en vergelijkt: [vergelijken met meerdere klasse classificaties: erkenning Letter ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> een diagram waarin u een overzicht van Hallo-mogelijkheden van Machine Learning Studio, Zie toodownload en het afdrukken [overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Versies van machine learning
### <a name="supervised"></a>Onder supervisie
Leren met supervisie algoritmen voorspellingen op basis van een reeks voorbeelden. Historische aandelenkoersen kunnen bijvoorbeeld gebruikte toohazard wat op prijzen in de toekomst zijn. Elk voorbeeld gebruikt voor training is gelabeld met Hallo-waarde van belang: in dit geval Hallo aandelenkoersen. Een algoritme leren met supervisie zoekt naar patronen in deze waardelabels. Het kan gebruiken informatie die van belang kan zijn: Hallo dag van week hello, Hallo seizoen, financiële gegevens van het bedrijf hello, Hallo type branche, Hallo aanwezigheid van verstoren geopolitieke gebeurtenissen — en elk algoritme eruitziet voor verschillende soorten patronen. Nadat Hallo-algoritme heeft Hallo best patroon kan worden gevonden, wordt gebruikt dat patroon toomake voorspellingen voor zonder label testgegevens: morgen prijzen.

Leren met supervisie is een populair en nuttige van machine learning. Met één uitzondering, worden alle Hallo-modules in Azure Machine Learning supervisie learning-algoritmen. Er zijn verschillende specifieke leren met supervisie-typen die worden vertegenwoordigd in Azure Machine Learning: classificatie, regressie en afwijkingsdetectie detectie.

* **Classificatie**. Wanneer gegevens hello worden gebruikt toopredict een categorie, leren met supervisie is een afkorting classificatie. Dit is Hallo geval bij het toewijzen van een afbeelding als een afbeelding van een 'cat' of een 'aquaduct'. Wanneer er slechts twee keuzes, deze wordt aangeroepen **tweeklasse** of **binomiale classificatie**. Wanneer er meer categorieën als bij de voorspelling van Hallo winnaar van Hallo NCAA maart Madness toernooi, dit probleem wordt ook wel **meerdere klasse classificatie**.
* **Regressie**. Wanneer u een waarde wordt net als bij aandelenkoersen wordt voorspeld, leren met supervisie regressie genoemd.
* **Afwijkingsdetectie**. Soms is hello doel tooidentify gegevenspunten die gewoon ongebruikelijk zijn. Fraude te detecteren, bijvoorbeeld zijn een bestedingslimiet patronen maximaal ongebruikelijke creditcard verdacht. Hallo mogelijke variaties zijn dus talrijke en Hallo training voorbeelden dus enkele, is het niet haalbaar toolearn welke frauduleuze activiteit ziet eruit als. De benadering waarmee afwijkingsdetectie toosimply is meer informatie over welke normale activiteit eruit (met behulp van een niet-frauduleuze transacties geschiedenis) en identificeren van alles die aanzienlijk verschilt.

### <a name="unsupervised"></a>Zonder supervisie
Zonder supervisie learning hebben gegevenspunten geen labels worden gekoppeld. In plaats daarvan learning Hallo doel van een zonder supervisie-algoritme is hello om gegevens te ordenen op sommige toodescribe of manier de structuur. Dit kan betekenen dat het groeperen in clusters of het vinden van de verschillende manieren van complexe gegevens bekijkt, zodat het eenvoudiger of meer geordend wordt weergegeven.

### <a name="reinforcement-learning"></a>Versterking learning
Versterking weten haalt Hallo algoritme toochoose een actie in antwoord tooeach gegevenspunt. Hallo leeralgoritme ontvangt ook een derden signaal korte tijd later, die aangeeft hoe goed Hallo besluit is.
Op basis hiervan Hallo algoritme Hiermee wijzigt u de strategie voor de volgorde tooachieve Hallo hoogste derden. Er zijn momenteel geen versterking learning-algoritme-modules in Azure Machine Learning. Versterking learning is gemeenschappelijk in robotics, waarbij Hallo reeks sensormetingen op één punt in tijd een gegevenspunt en Hallo-algoritme moet de volgende actie van Hallo robot kiezen. Het is ook dat een natuurlijke geschikt voor Internet der dingen toepassingen.

## <a name="considerations-when-choosing-an-algorithm"></a>Overwegingen bij het kiezen van een algoritme
### <a name="accuracy"></a>Nauwkeurigheid
Ophalen van de meest nauwkeurige antwoord Hallo mogelijk niet altijd nodig.
Een benadering is soms voldoende, afhankelijk van wat u wilt gebruiken. Als dit Hallo geval is, hebt u mogelijk kunnen toocut uw verwerkingstijd aanzienlijk door bevalt meer geschatte methoden. Een ander voordeel van methoden met meer bij benadering is dat ze natuurlijk vaak voorkomen [overfitting](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Trainingstijd
Hallo aantal minuten of uren nodig tootrain die een model veel van de algoritmen is. Vaak sterk training tijd is gekoppeld aan nauwkeurigheid: een doorgaans wordt meegestuurd met Hallo andere. Bovendien zijn sommige algoritmen gevoeliger toohello aantal gegevenspunten dan andere.
Wanneer het tijd is beperkt kunt deze Hallo keuze van algoritme, station, vooral wanneer Hallo gegevensset groot is.

### <a name="linearity"></a>Lineariteit
Veel van de machine learning-algoritmen maken gebruik van lineariteit. Lineaire classificatie algoritmen wordt ervan uitgegaan dat klassen kunnen worden gescheiden door een lineaire (of de hogere-dimensionale analoge). Dit zijn logistic regression en vector machines ondersteunen (zoals geïmplementeerd in Azure Machine Learning).
Lineaire regressie algoritmen wordt ervan uitgegaan dat gegevenstrends een lineaire volgen. Deze veronderstellingen niet nadelig voor sommige problemen, maar ze op andere omlaag nauwkeurigheid meenemen.

![Niet-lineaire klasse grens][1]

***Niet-lineaire klasse grens*** *-afhankelijk te zijn van een algoritme lineaire classificatie zou leiden tot nauwkeurigheid laag*

![Gegevens met een niet-lineaire trend][2]

***Gegevens met een niet-lineaire trend*** *-met een methode lineaire regressie genereert veel fouten groter is dan nodig*

Lineaire algoritmen zijn ondanks hun gevaren zeer populair is een eerste regel van een aanval. Ze hebben vaak toobe algoritmisch eenvoudig en snel te trainen.

### <a name="number-of-parameters"></a>Aantal parameters
Parameters zijn Hallo knoppen een wetenschappelijk gegevens tooturn opgehaald bij het instellen van een algoritme. Ze zijn getallen die invloed hebben op Hallo-algoritme gedrag, zoals fouttolerantie of het aantal iteraties of opties tussen varianten van het gedrag van Hallo-algoritme. Hallo trainingstijd en de nauwkeurigheid van het Hallo-algoritme mag soms behoorlijk gevoelige toogetting alleen Hallo instellingen. Algoritmen met grote aantallen parameters moeten normaal Hallo meest proefversie en fout toofind een goede combinatie.

Er is ook een [parameter sweeping](machine-learning-algorithm-parameters-optimize.md) module blok in Azure Machine Learning die probeert automatisch alle parametercombinaties ongeacht samenvattingen die u kiest. Dit is een uitstekende manier toomake ervoor dat u Hallo parameter ruimte hebt omspannen, Hallo tijd die nodig is tootrain een model verhoogt exponentieel met Hallo aantal parameters.

Hallo is opwaartse dat veel parameters doorgaans met geeft aan dat een algoritme meer flexibiliteit heeft. Zeer goede nauwkeurigheid ontstaan vaak. Opgegeven vindt u Hallo combinatie van instellingen.

### <a name="number-of-features"></a>Aantal functies
Voor bepaalde soorten gegevens, kan het aantal functies Hallo zeer grote vergeleken toohello aantal gegevenspunten zijn. Dit is vaak Hallo geval met genetica of tekstgegevens. groot aantal functies Hallo kunt bog omlaag sommige learning-algoritmen waardoor training unfeasibly lange tijd. Ondersteuning Vector Machines zijn bijzonder geschikt toothis geval (Zie hieronder).

### <a name="special-cases"></a>Bijzondere gevallen
Sommige learning-algoritmen zorg bepaalde veronderstellingen over de structuur Hallo Hallo gegevens of Hallo gewenst resultaten. Als u een die past bij uw behoeften vinden kunt, krijgt deze u meer bruikbare resultaten, meer nauwkeurige prognoses of sneller training.

| **Algoritme** | **Nauwkeurigheid** | **Trainingstijd** | **Lineariteit** | **Parameters** | **Opmerkingen bij de** |
| --- |:---:|:---:|:---:|:---:| --- |
| **Classificatie van de twee-klasse** | | | | | |
| [logistic regression](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [besluit forest](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [besluit jungle](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Lage geheugengebruik: |
| [gestimuleerd beslissingsstructuur](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Groot geheugengebruik: |
| [neurale netwerk](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[Extra aanpassingen zijn mogelijk](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [gemiddelde perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [ondersteuning voor vectormachine](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Goede voor grote functiesets |
| [lokaal grondige ondersteuning vectormachine](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Goede voor grote functiesets |
| [De Bayes point machine](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Meerdere klasse-classificatie** | | | | | |
| [logistic regression](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [besluit forest](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [besluit jungle](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Lage geheugengebruik: |
| [neurale netwerk](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[Extra aanpassingen zijn mogelijk](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [One-v-all](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Controleer de eigenschappen van Hallo tweeklasse methode geselecteerd |
| **Regressie** | | | | | |
| [Lineair](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [Bayesiaanse lineair](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [besluit forest](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [gestimuleerd beslissingsstructuur](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Groot geheugengebruik: |
| [snelle forest kwantiel](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Distributies in plaats van punt voorspellingen |
| [neurale netwerk](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[Extra aanpassingen zijn mogelijk](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [POISSON](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Technisch logboek-lineaire. Voor het voorspellen van aantallen |
| [rangtelwoord](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |Voor het voorspellen van positie ordenen |
| **Detectie van afwijkingen** | | | | | |
| [ondersteuning voor vectormachine](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Met name geschikt voor grote functiesets |
| [PCA-gebaseerd anomaliedetectie](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Een clustering-algoritme |

**Algoritme-eigenschappen:**

**●** -uitstekende nauwkeurigheid, snelle training tijden en Hallo gebruik van lineariteit toont

**○** -goede nauwkeurigheid en matig training tijden toont

## <a name="algorithm-notes"></a>Opmerkingen bij de algoritme
### <a name="linear-regression"></a>Lineaire regressie
Zoals eerder vermeld [lineaire regressie](https://msdn.microsoft.com/library/azure/dn905978.aspx) past een set van regel (of vlak of hyperplane) een toohello gegevens. Er is een werkpaard, eenvoudig en snel, maar dit kan zeer eenvoudig voor bepaalde problemen.
Schakel dit selectievakje in voor een [lineaire regressie zelfstudie](machine-learning-linear-regression-in-azure.md).

![Gegevens met een lineaire trend][3]

***Gegevens met een lineaire trend***

### <a name="logistic-regression"></a>Logistic regression
Hoewel het verwarrende 'regressie' hello naam bevat, is logistic regression daadwerkelijk een krachtig hulpprogramma voor [tweeklasse](https://msdn.microsoft.com/library/azure/dn905994.aspx) en [multiklasse](https://msdn.microsoft.com/library/azure/dn905853.aspx) classificatie. Het is snel en eenvoudig. Hallo fact dat wordt gebruikt een van '-gevormde curve in plaats van een lineaire maakt het naadloos voor gegevens verdelen in groepen. Logistic regression biedt lineaire klassengrenzen zorg wanneer u gebruikt, er dus dat een lineaire benadering is iets dat die u kunt leven.

![Logistic regression tootwo klasse gegevens met één functie][4]

***Een logistic regression tootwo-klasse-gegevens met één functie*** *-grens van de klasse is Hallo-punt op welke Hallo logistic curve net zo dicht tooboth klassen is*

### <a name="trees-forests-and-jungles"></a>Structuren en forests jungles
Besluit forests ([regressie](https://msdn.microsoft.com/library/azure/dn905862.aspx), [tweeklasse](https://msdn.microsoft.com/library/azure/dn906008.aspx), en [multiklasse](https://msdn.microsoft.com/library/azure/dn906015.aspx)), besluit jungles ([tweeklasse](https://msdn.microsoft.com/library/azure/dn905976.aspx) en [multiklasse](https://msdn.microsoft.com/library/azure/dn905963.aspx)), en boosted decision trees ([regressie](https://msdn.microsoft.com/library/azure/dn905801.aspx) en [tweeklasse](https://msdn.microsoft.com/library/azure/dn906025.aspx)) zijn alle op basis van beslissingsstructuren, een fundamenteel machine learning-concept. Er zijn veel varianten van beslissingsstructuren, maar ze allemaal dezelfde dingen doen: Hallo functie ruimte onderverdelen in regio's met voornamelijk Hallo hetzelfde label. Deze kunnen gebieden van consistente categorie of van een constante waarde, afhankelijk van of er zijn geen classificatie- of regressiemodel zijn.

![Beslissingsstructuur verdeelt een spatie functie][5]

***Een beslissingsstructuur verdeelt de ruimte van een functie in regio's van ongeveer uniform waarden***

Omdat een spatie functie kan worden onderverdeeld in willekeurig kleine regio's, is het eenvoudig tooimagine verdelen fijn voldoende toohave één gegevenspunt per regio. Dit is een uiterst voorbeeld van te. In de volgorde tooavoid zijn dit een groot aantal structuren speciale wiskundige zorgvuldig genomen samengesteld dat Hallo structuren niet zijn gecorreleerd. Hallo gemiddelde van deze 'besluit forest' is een structuur die wordt te voorkomen. Besluit forests kunnen veel geheugen gebruiken. Decision jungles zijn een variant die minder geheugen op Hallo kosten van iets meer trainingstijd verbruikt.

Te voorkomen gestimuleerd beslissingsstructuren door te beperken hoe vaak ze kunnen onderverdelen en hoe weinig gegevenspunten zijn toegestaan in elke regio. Het algoritme vormt een reeks van structuren, die elk leert om te compenseren voor Hallo fout door Hallo structuur voordat achtergelaten. Hallo-resultaat is een zeer nauwkeurig cursist die doorgaans toouse een grote hoeveelheid geheugen. Voor volledige technische beschrijving Hallo, Bekijk [Friedman van oorspronkelijke papier](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[Snelle forest kwantiel regressie](https://msdn.microsoft.com/library/azure/dn913093.aspx) is een variatie beslissingsstructuren voor Hallo uitzonderlijke gevallen waarin u wilt weten niet alleen Hallo typische () mediaanwaarde van Hallo gegevens binnen een regio, maar ook de distributie in de vorm Hallo van quantiles.

### <a name="neural-networks-and-perceptrons"></a>Neural networks en perceptrons
Neural networks zijn brain-geïnspireerd learning-algoritmen die betrekking hebben op [multiklasse](https://msdn.microsoft.com/library/azure/dn906030.aspx), [tweeklasse](https://msdn.microsoft.com/library/azure/dn905947.aspx), en [regressie](https://msdn.microsoft.com/library/azure/dn905924.aspx) problemen. Ze worden geleverd in een oneindige RAS, maar Hallo neural netwerken in Azure Machine Learning zijn alle Hallo vorm van gerichte acyclische grafieken. Dat betekent dat invoer functies worden doorgegeven doorsturen (nooit terug) via een reeks van lagen voordat het wordt omgezet in de uitvoer. Invoer worden in elke laag in verschillende combinaties, opgeteld en doorgegeven aan de volgende laag Hallo gewogen. Deze combinatie van eenvoudige berekeningen resulteert in de mogelijkheid toolearn geavanceerde klasse grenzen en gegevens trends schijnbaar door verwerkt Magic-pakket. Veel gelaagd netwerken van de sortering uitvoeren Hallo 'grondige kennis' die helpt u bij het zo veel tech reporting en sciencefiction.

Deze hoge prestaties niet afkomstig zijn gratis al. Neural networks kunnen duren voordat een tootrain lang, met name voor grote gegevenssets met een groot aantal functies. Ze hebben ook meer parameters dan de meeste algoritmen, wat betekent dat de parameter sweeping wordt uitgebreid Hallo trainingstijd veel.
En voor deze overachievers die te wensen[opgeven van hun eigen netwerkstructuur](http://go.microsoft.com/fwlink/?LinkId=402867), de mogelijkheden zijn inexhaustible.

![Grenzen geleerd door neural networks][6]
***Hallo grenzen geleerd door neural networks complex zijn en onregelmatige***

Hallo [tweeklasse gemiddeld perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) neural networks antwoord tooskyrocketing training tijden is. Een netwerkstructuur waarmee lineaire klassengrenzen wordt gebruikt. Is bijna primitieve door de hedendaagse standaarden, maar er is een lang geschiedenisgegevens krachtig te werken en klein genoeg toolearn snel is.

### <a name="svms"></a>SVMs
Ondersteuning vector machines (SVMs) vinden Hallo bevindt die afscheiding van klassen door als breed marge mogelijk. Wanneer twee klassen Hallo duidelijk kunnen niet worden gescheiden, vinden Hallo algoritmen Hallo best grens ze kunnen. Zoals vermeld in Azure Machine Learning, Hallo [tweeklasse SVM](https://msdn.microsoft.com/library/azure/dn905835.aspx) doet dit met een lineaire. (In SVM spreekt, worden er gebruikt een lineaire kernel.) Omdat deze lineaire aanpassing maakt, is het kunnen toorun vrij snel. Waar deze uitkomst is met de functie intensief gegevens, zoals tekst of Toepassingsgeoriënteerde. In deze gevallen zijn SVMs kunnen tooseparate klassen sneller en met minder overfitting dan de meeste andere algoritmen bovendien toorequiring een kleine hoeveelheid geheugen.

![Ondersteuning vector machine klasse grens][7]

***De grens van een typische ondersteuning vector machine klasse maximaliseert de Hallo marge twee klassen te scheiden***

Een ander product van Microsoft Research Hallo [tweeklasse lokaal grondige SVM](https://msdn.microsoft.com/library/azure/dn913070.aspx) is een niet-lineaire variant van SVM die de meeste Hallo snelheid en efficiëntie van Hallo lineaire versie behoudt. Dit is ideaal voor gevallen Hallo lineaire aanpak waar geen nauwkeurige genoeg antwoorden geeft. Hallo ontwikkelaars bewaard deze snel door de Hallo probleem in een aantal kleine lineaire SVM problemen analyseren. Lees Hallo [volledige beschrijving](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) voor Hallo informatie over hoe ze opgehaald uit deze methode.

Gebruik van een slimme extensie van niet-lineaire SVMs Hallo [één klasse SVM](https://msdn.microsoft.com/library/azure/dn913103.aspx) een grens die nauw geeft een overzicht van de volledige gegevensset hello wordt getekend. Dit is handig voor afwijkingsdetectie. De nieuwe gegevenspunten die ver buiten die grens vallen zijn ongebruikelijke genoeg toobe opmerkelijk.

### <a name="bayesian-methods"></a>Bayesiaanse methoden
Bayesiaanse methoden hebben een zeer wenselijk kwaliteit: ze te voorkomen. Ze doen dit met bepaalde veronderstellingen tevoren over Hallo waarschijnlijk distributie van Hallo antwoord. Een andere bijkomend gevolg van deze benadering is dat ze heel weinig parameters hebben. Azure Machine Learning heeft beide Bayesiaanse algoritmen voor beide classificatie (['Two-class Bayes point machine](https://msdn.microsoft.com/library/azure/dn905930.aspx)) en regressie ([Bayesiaanse lineaire regressie](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Houd er rekening mee dat deze wordt ervan uitgegaan dat Hallo gegevens kunnen worden gesplitst of aan een lineaire voldoen.

De Bayes point-machines zijn op een historische notitie ontwikkeld door Microsoft Research. Ze hebben sommige uitzonderlijk mooi vormgegeven theoretische werk achterliggende. Hallo geïnteresseerd studenten is gerichte toohello [oorspronkelijke artikel in JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) en een [begrijpelijke manier mee blog door Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Gespecialiseerde algoritmen
Als u een zeer specifiek doel hebt u mogelijk mee. Er zijn in Azure Machine Learning-verzameling hello, algoritmen die zijn gespecialiseerd in:

- voorspelling rangschikken ([ordinale regressie](https://msdn.microsoft.com/library/azure/dn906029.aspx)),
- voorspelling tellen ([Poisson regressie](https://msdn.microsoft.com/library/azure/dn905988.aspx)),
- afwijkingsdetectie (één op basis van [analyse van de belangrijkste onderdelen](https://msdn.microsoft.com/library/azure/dn913102.aspx) en op basis van een [vectormachine ondersteuning](https://msdn.microsoft.com/library/azure/dn913103.aspx)s)
- Clustering ([K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![PCA-gebaseerd anomaliedetectie][8]

***PCA-gebaseerd anomaliedetectie*** *-Hallo meeste Hallo gegevens worden onderverdeeld in een stereotypical verdeling; punten die aanzienlijk afwijken van dit distributiepunt verdacht zijn*

![Gegevensset met K-means gegroepeerd][9]

***Een gegevensset worden onderverdeeld in vijf clusters met K-means***

Er is ook een ensemble [one-v-all multiklassen classificatie](https://msdn.microsoft.com/library/azure/dn905887.aspx), welk probleem einden Hallo N klasse classificatie N-1 tweeklasse classificatie problemen. Hallo nauwkeurigheid en trainingstijd lineariteit eigenschappen worden bepaald door Hallo tweeklasse classificaties gebruikt.

![Twee klasse classificaties gecombineerd tooform een classificatie drie-klasse][10]

***Een combinatie van twee klasse classificaties combineren tooform een classificatie drie-klasse***

Azure Machine Learning bevat ook toegang tooa krachtige machine learning framework onder de titel Hallo van [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
Een code defies categorisatie hier, omdat deze zowel classificatie en regressie problemen lezen kan en zelfs van gegevens gedeeltelijk zonder label leren kan. U kunt deze configureren toouse een uit een aantal learning-algoritmen, verlies van functies en algoritmen voor optimalisatie. Het is ontworpen van Hallo gemalen up toobe efficiënte, parallelle en zeer snel. Heel groot functiesets moeiteloos duidelijk verwerkt.
Gestart en door Microsoft Research van eigen John Langford geleid, is een code een formule één vermelding in een veld van stock auto-algoritmen. Niet elk probleem geschikt is voor een code, maar als het account van jou is, kan het zijn de moeite waard tooclimb het leerproces op de interface. Het is ook beschikbaar als [zelfstandige open-source code](https://github.com/JohnLangford/vowpal_wabbit) in verschillende talen.

## <a name="more-help-with-algorithms"></a>Meer hulp bij algoritmen
* Zie voor een downloadbare infographic die beschrijving algoritmen en voorbeelden, [downloadbare Infographic: Machine learning-algoritme voorbeelden voor alledaagse](machine-learning-basics-infographic-with-algorithm-examples.md).
* Zie voor een lijst door de categorie van alle Hallo machine learning-algoritmen die beschikbaar zijn in Azure Machine Learning Studio [Model initialiseren] [ initialize-model] in de Help van de Module en Hallo Machine Learning Studio algoritme.
* Zie voor een volledige alfabetische lijst van algoritmen en modules in Azure Machine Learning Studio [lijst A-Z van Machine Learning Studio-modules] [ a-z-list] in de Help van de Module en Machine Learning Studio-algoritme.
* een diagram waarin u een overzicht van Hallo-mogelijkheden van Azure Machine Learning Studio, Zie toodownload en het afdrukken [overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
