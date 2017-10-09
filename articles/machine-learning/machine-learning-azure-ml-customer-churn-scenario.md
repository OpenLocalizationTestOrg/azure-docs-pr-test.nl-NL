---
title: aaaAnalyzing klant verloop met behulp van Machine Learning | Microsoft Docs
description: "Casestudy van een geïntegreerde model voor het analyseren en score berekenen voor verloop van de klant te ontwikkelen"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Traject van de klant analyseren met Azure Machine Learning
## <a name="overview"></a>Overzicht
Dit artikel bevat een verwijzing implementatie van een klant verloop analysis project is gebouwd met behulp van Azure Machine Learning. In dit artikel wordt besproken gekoppelde algemene modellen voor het oplossen van holistische Hallo probleem van industriële customer verloop. We ook Hallo nauwkeurigheid van modellen die zijn gebouwd met behulp van Machine Learning meten en we routebeschrijving voor verdere ontwikkeling beoordelen.  

### <a name="acknowledgements"></a>Bevestigingen
Dit experiment is ontwikkeld en getest door Serge Berger, Principal gegevens wetenschappelijk bij Microsoft en Roger Barga, voorheen Product Manager van Microsoft Azure Machine Learning. Hello Azure documentatieteam dank erkent hun expertise en ze Bedankt voor het delen van dit document.

> [!NOTE]
> Hallo-gegevens die worden gebruikt voor dit experiment is niet openbaar beschikbaar. Zie voor een voorbeeld van hoe een machine learning toobuild model voor verloop analyse: [Retail verloop model sjabloon](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>Hallo probleem van klanten verloop
Bedrijven in Hallo consumer markt en in alle sectoren voor ondernemingen hebben toodeal met verloop. Soms verloop uitzonderlijk veel en beleidsbeslissingen beïnvloedt. Hallo traditionele oplossing is toopredict investeringsneiging van hoge churners en hun behoeften via een service concierge marketingcampagnes, of door het toepassen van speciale dispensaties. Deze methoden kunnen variëren op branche tooindustry en zelfs op een bepaalde consumer cluster tooanother binnen één industry (bijvoorbeeld telecommunicatie).

Hallo gemeenschappelijke factor is dat bedrijven toominimize deze inspanningen van speciale klant bewaren moeten. Een natuurlijke methodologie zou worden tooscore elke klant met Hallo kans van verloop en dus adres Hallo bovenste N die zijn. Hallo belangrijkste klanten mogelijk de Hallo meest winstgevend die zijn; bijvoorbeeld, meer geavanceerde scenario's, een functie winst in dienst is tijdens het Hallo-selectie van kandidaten voor speciale dispensatie. Deze overwegingen zijn echter slechts een deel van Hallo holistische strategie voor het omgaan met verloop. Bedrijven hebben ook tootake in account risico (en bijbehorende risicotolerantie) Hallo niveau en de kosten van Hallo tussenkomst en aannemelijke klant segmentering.  

## <a name="industry-outlook-and-approaches"></a>Bedrijfstak outlook en methoden
Geavanceerde verwerking van verloop is een teken van een goed ontwikkelde industrie. Hallo klassiek voorbeeld is Hallo telecommunicatie branche waarin abonnees bekende toofrequently overschakelen van één provider tooanother zijn. Deze vrijwillige verloop zijn de belangrijkste zorgen. Bovendien providers aanzienlijke kennis hebben verzameld over *verloop van stuurprogramma's*, die zijn Hallo factoren die klanten station tooswitch.

Telefoon of apparaat keuze is voor het exemplaar een bekende stuurprogramma van het verloop in Hallo mobiele telefoon bedrijven. Als gevolg hiervan is een populair beleid toosubsidize Hallo prijs van een toestel voor nieuwe abonnees en klanten voor een upgrade voor een volledige prijs tooexisting kostenberekening. Dit beleid heeft in het verleden hebben toocustomers hopping van één provider tooanother tooget een nieuwe korting die op zijn beurt is gevraagd providers toorefine hun strategieën geleid.

Hoge volatiliteit in de offerings telefoon is een factor waardoor zeer snel modellen van het verloop op basis van huidige telefoon-modellen. Mobiele telefoons zijn bovendien niet alleen de apparaten telecommunicatie; ze zijn ook wijze instructies (Overweeg het Hallo iPhone) en deze sociale variabelen zijn buiten Hallo bereik van reguliere telecommunicatie gegevenssets.

Hallo resultaat voor modellering is dat u een geluid beleid kan niet ontwerpen gewoon doordat bekende redenen voor het verloop. Een strategie voor een continue modellering, met inbegrip van klassieke modellen die categorische variabelen (zoals beslissingsstructuren kwantificeren) is in feite **verplichte**.

Met behulp van grote gegevenssets op hun klanten, uitvoert organisaties big data-analyses (met name verloop detectie op basis van big data) als een effectieve manier toohello probleem. U vindt meer informatie over Hallo big data benadering toohello probleem van het verloop in Hallo aanbevelingen voor ETL-sectie.  

## <a name="methodology-toomodel-customer-churn"></a>Methodologie toomodel klant verloop
Een algemene probleemoplossing proces toosolve klant verloop wordt beschreven in cijfers 1-3:  

1. Een risicomodel kunt u tooconsider invloed van acties kans en risico's.
2. Een model tussenkomst, kunt u tooconsider Hallo niveau van tussenkomst kan invloed kans op Hallo van verloop en Hallo bedrag van de waarde van de klant-levensduur (CLV).
3. Deze analyse gepaard tooa kwalitatieve analyse die geëscaleerde tooa proactieve marketingcampagne die gericht is op de klant segmenten toodeliver Hallo optimale aanbieding.  

![][1]

Deze aanpak sturen ogende Hallo aanbevolen manier tootreat verloop is, maar wordt geleverd met complexiteit: we hebben toodevelop een meerdere model archetype en tracering afhankelijkheden tussen Hallo-modellen. Hallo interactie tussen modellen kunt worden ingekapseld, zoals wordt weergegeven in het volgende diagram Hallo:  

![][2]

*Afbeelding 4: Unified met meerdere modellen archetype*  

Interactie tussen Hallo modellen is sleutel als we toodeliver een holistische aanpak toocustomer bewaren. Elk model vermindert noodzakelijkerwijs gedurende een bepaalde periode; Hallo-architectuur is daarom een impliciete lus (vergelijkbaar toohello archetype ingesteld door Hallo heldere DM datamining standaard [***3***]).  

Hallo is algehele cyclus van de risico-besluit-marketing segmentering/afbreken nog steeds een algemene structuur, van toepassing toomany zakelijke problemen is. Verloop analyse is gewoon een sterke vertegenwoordiger van deze groep van problemen, omdat deze alle Hallo-eigenschappen van complexe zakelijke problemen die niet in een vereenvoudigde voorspellende oplossing staat vertoont. Hallo sociale aspecten van Hallo benadering van moderne toochurn vooral niet in Hallo benadering zijn gemarkeerd, maar Hallo sociale aspecten worden ingekapseld in Hallo modellering archetype, zoals in een model.  

Hier een interessante toevoeging is big data-analyses. De hedendaagse telecommunicatie en retail bedrijven volledig worden gegevens verzameld over hun klanten en we kunnen eenvoudig voorzien die Hallo nodig voor meerdere model connectiviteit is een algemene trend, opgegeven trends zoals opkomende in de toekomst Hallo Internet der dingen en de alomtegenwoordige apparaten, waardoor business tooemploy smart-oplossingen met meerdere lagen.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Hallo modelleren archetype in Machine Learning Studio implementeren
Opgegeven Hallo probleem hierboven wordt beschreven, wat is Hallo aanbevolen manier tooimplement een geïntegreerde modellen en scoreprofiel benadering? In deze sectie wordt gedemonstreerd hoe we dit doen met behulp van Azure Machine Learning Studio.  

Hallo met meerdere modellen aanpak is een moet bij het ontwerpen van een globale archetype voor verloop. Zelfs Hallo score berekenen (voorspellende) deel uit van Hallo benadering moet met meerdere modellen.  

Hallo volgende diagram toont Hallo prototype dat wordt gemaakt, die de veiligheidsmaatregelen voor vier scoreprofiel algoritmen in Machine Learning Studio toopredict verloop. Hallo reden voor het gebruik van een benadering van meerdere model is niet alleen toocreate ensemble classificatie tooincrease nauwkeurig, maar ook tooprotect tegen te veel aanpassen en tooimprove prescriptieve Functieselectie.  

![][3]

*Afbeelding 5: Prototype van een benadering modelleren verloop*  

Hallo bevatten volgende secties meer informatie over Hallo prototype score model dat wordt geïmplementeerd met behulp van Machine Learning Studio.  

### <a name="data-selection-and-preparation"></a>Gegevensselectie en voorbereiding
Hallo gegevens gebruikt toobuild Hallo modellen en score klanten is verkregen van een verticale CRM-oplossing met Hallo verborgen tooprotect klant gegevensprivacy. Hallo gegevens bevat informatie over 8.000 abonnementen in Hallo VS, en worden drie bronnen gecombineerd: inrichting gegevens (abonnement metagegevens), activiteitsgegevens (informatie over het gebruik van Hallo system) en klantgegevens voor ondersteuning. Hallo gegevens omvat niet alle zakelijke gerelateerde gegevens over Hallo klanten; bijvoorbeeld, omvat het geen loyaliteit metagegevens of een tegoed scores.  

Ter vereenvoudiging zijn ETL en processen voor opschonen van gegevens buiten het bereik omdat we ervan uitgaan dat het voorbereiden van gegevens is al is gedaan elders.   

Functieselectie voor modellering is gebaseerd op voorlopige significante scoren van Hallo reeks variabelen, opgenomen in het Hallo-proces dat wordt gebruikt Hallo willekeurige forest module. Voor de implementatie van de Hallo in Machine Learning Studio berekend we Hallo gemiddelde, de mediaan en de bereiken voor representatieve functies. Bijvoorbeeld, hebben we statistische functies voor Hallo kwalitatieve gegevens, zoals de minimale en maximale waarden voor gebruikersactiviteit toegevoegd.    

We vastgelegd tijdelijke informatie voor Hallo meest recente zes maanden ook. Gegevens van één jaar geanalyseerd en we tot stand gebracht zelfs als er sprake statistisch aanzienlijke trends was, wordt Hallo effect op verloop aanzienlijk verminderd na zes maanden.  

Hallo belangrijkste is dat Hallo hele proces, inclusief ETL, feature selection en modelleren in Machine Learning Studio, met behulp van gegevensbronnen in Microsoft Azure is geïmplementeerd.   

Hallo volgende afbeeldingen laten zien Hallo gegevens dat is gebruikt.  

![][4]

*Afbeelding 6: Fragment van een gegevensbron (verborgen)*  

![][5]

*Afbeelding 7: Functies opgehaald uit de gegevensbron*
 

> Houd er rekening mee dat deze gegevens persoonlijke zijn en daarom Hallo model en gegevens kunnen niet worden gedeeld.
> Voor een vergelijkbaar model met openbaar beschikbare gegevens, ziet in dit voorbeeld experimenteren in Hallo [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [Telco klant verloop](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> toolearn meer informatie over hoe u een verloop Analytics-model met behulp van Cortana Intelligence Suite kunt implementeren, wordt ook aangeraden [in deze video](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) door Senior Program Manager Westerse Hyong Tok. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Die worden gebruikt in het Hallo-prototype
We Hallo na vier machine learning-algoritmen gebruikt toobuild Hallo prototype (geen aanpassing):  

1. Logistic regression (LR)
2. Gestimuleerd beslissingsstructuur (BT)
3. Gemiddelde perceptron (AP)
4. Ondersteuning voor vectormachine (SVM)  

Hallo wordt volgende diagram een deel van Hallo experiment ontwerpoppervlak, waarmee wordt aangegeven Hallo-reeks in welke Hallo modellen zijn gemaakt:  

![][6]  

*Afbeelding 8: Modellen maken in Machine Learning Studio*  

### <a name="scoring-methods"></a>Score berekenen voor methoden
We berekend Hallo vier modellen met behulp van een gegevensset gelabelde training.  

Score berekenen voor gegevensset tooa vergelijkbare model gebouwd met behulp van de desktop edition Hallo van SAS Enterprise mijnwerkers 12 Hallo ook verzonden. We gemeten Hallo nauwkeurig Hallo SAS-model en alle vier Machine Learning Studio-modellen.  

## <a name="results"></a>Resultaten
In deze sectie geven we onze bevindingen over Hallo nauwkeurig Hallo modellen, gebaseerd op Hallo score berekenen voor gegevensset.  

### <a name="accuracy-and-precision-of-scoring"></a>Nauwkeurigheid en precisie van score berekenen
Hallo-implementatie in Azure Machine Learning is over het algemeen achter SAS nauwkeurig ongeveer 10-15% (gebied onder Curve of AUC).  

Hallo belangrijkste metrische gegevens in verloop is echter Hallo misclassification frequentie: dat wil zeggen van Hallo bovenste N churners als voorspelde door Hallo classificatie, wie daadwerkelijk heeft **niet** verloop en nog ontvangen speciale behandeling? Hallo volgende diagram worden de frequentie van deze misclassification voor alle Hallo modellen vergeleken:  

![][7]

*Afbeelding 9: Passau prototype gebied onder curve*

### <a name="using-auc-toocompare-results"></a>Met behulp van AUC toocompare resultaten
Gebied onder Curve (AUC) is een waarde die staat voor een globale meting van *Afscheidbaarheid* tussen scores voor positieve en negatieve populaties Hallo-distributies. Het is vergelijkbaar toohello traditionele ontvanger Operator kenmerk (ROC) grafiek, maar één belangrijk verschil is dat Hallo AUC metriek vereist niet dat u een drempelwaarde toochoose. In plaats daarvan Hallo resultaten worden samengevat via **alle** keuzemogelijkheden. Daarentegen Hallo traditionele ROC grafiek toont Hallo positief frequentie op Hallo verticale as en Hallo false positief tarief op Hallo horizontale as en Hallo classificatie drempelwaarde varieert.   

AUC wordt doorgaans gebruikt als een maatstaf voor waard voor verschillende algoritmen (of andere systemen) omdat deze modellen toobe vergeleken met behulp van hun AUC-waarden toestaat. Dit is een populair benadering in sectoren zoals meteorologie en biosciences. Dus vertegenwoordigt AUC een populaire hulpprogramma voor beoordeling van de prestaties van de classificatie.  

### <a name="comparing-misclassification-rates"></a>Misclassification tarieven vergelijken
We vergeleken Hallo misclassification tarieven op Hallo gegevensset betrokken met behulp van Hallo CRM-gegevens van ongeveer 8000 abonnementen.  

* Hallo SAS misclassification snelheid is 10-15%.
* Hallo Machine Learning Studio misclassification snelheid is 15-20% voor Hallo top 200 en 300 churners.  

In Hallo telecommunicatie industrie is het belangrijk tooaddress alleen klanten die hebben Hallo hoogste risico toochurn door het aanbieden van deze een service concierge of andere speciale behandeling. In dat opzicht realiseert Hallo Machine Learning Studio implementatie resultaten één lijn met Hallo SAS-model.  

Door Hallo token dezelfde, nauwkeurigheid belangrijker dan de precisie is omdat we voornamelijk geïnteresseerd bent in de potentiële churners correct te classificeren.  

Hallo volgende diagram uit Wikipedia (Engelstalig) ziet Hallo relatie in een afbeelding levendige, gemakkelijk te begrijpen:  

![][8]

*Afbeelding 10: Afweging tussen nauwkeurigheid en juistheid*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Nauwkeurigheid en juistheid resultaten voor gestimuleerd decision tree model
Hallo volgende diagram geeft Hallo onbewerkte resultaat is van een score berekenen met behulp van Machine Learning-prototype Hallo voor Hallo boosted decision tree model die toobe Hallo nauwkeurigste tussen Hallo vier modellen wordt uitgevoerd:  

![][9]

*Afbeelding 11: Gestimuleerd decision tree model kenmerken*

## <a name="performance-comparison"></a>Vergelijking van de prestaties
We vergeleken Hallo snelheid waarmee gegevens is berekend met behulp van Hallo Machine Learning Studio modellen en een vergelijkbare model dat is gemaakt met behulp van bureaublad Hallo-editie van SAS Enterprise mijnwerkers 12.1.  

Hallo volgende tabel geeft een overzicht van de prestaties Hallo Hallo algoritmen:  

*Tabel 1. Algemene prestaties (nauwkeurigheid) Hallo-algoritmen*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| Gemiddelde Model |Hallo Best Model |Attenderen |Gemiddelde Model |

Hallo-modellen in Machine Learning Studio ver-loop SAS met 15-25% voor snelheid van kan worden uitgevoerd, maar de nauwkeurigheid grotendeels op nominaal werd gehost.  

## <a name="discussion-and-recommendations"></a>Discussie en aanbevelingen
In Hallo telecommunicatie industrie verschillende procedures tooanalyze is ontstaan verloop, met inbegrip van:  

* Afgeleid metrische gegevens voor vier fundamentele categorieën:
  * **Entiteit (bijvoorbeeld een abonnement)**. Algemene informatie over het Hallo-abonnement en/of de klant die Hallo onderwerp is van het verloop inrichten.
  * **Activiteit**. Alle informatie over het gebruik mogelijk die is gerelateerd toohello entiteit, bijvoorbeeld Hallo aantal aanmeldingen verkrijgen.
  * **Klantondersteuning**. Verzamelt gegevens van de klant ondersteuning logboeken tooindicate of Hallo abonnement heeft problemen of interacties met klant ondersteunen.
  * **Concurrerende en zakelijke gegevens**. Verkrijgen van mogelijk informatie over de klant hello (bijvoorbeeld kunnen zijn niet beschikbaar of harde tootrack).
* Urgentie toodrive Functieselectie gebruiken. Dit betekent dat Hallo boosted decision tree model is altijd een ordertoezegging benadering.  

Hallo gebruik van de volgende vier categorieën maakt Hallo illusie die een eenvoudige *deterministische* benadering, op basis van indexen notatie op redelijke factoren per categorie, moet klanten tooidentify risico voor verloop voldoende. Helaas, hoewel dit begrip aannemelijke lijkt, is een false begrip. Hallo reden is dat verloop is een tijdelijke effect Hallo factoren bijdragen toochurn zijn meestal tijdelijke status. Wat een klant tooconsider verlaten vandaag leidt kan afwijken morgen en zeker moeten verschillende zes maanden vanaf nu. Daarom een *probabilistische* model is noodzakelijk.  

Deze belangrijke observatie wordt vaak vergeten in bedrijf, in het algemeen een tooanalytics van business intelligence gebaseerde methode de voorkeur, voornamelijk omdat deze een eenvoudiger verkopen en admits eenvoudige automation.  

Echter, Hallo belofte van analyses met zelfservice met behulp van Machine Learning Studio is dat het Hallo vier categorieën van informatie, ingedeeld in de afdeling een waardevolle bron voor machine learning over verloop.  

Een andere interessante mogelijkheid binnenkort in Azure Machine Learning is Hallo mogelijkheid tooadd een aangepaste module toohello opslagplaats van vooraf gedefinieerde modules die al beschikbaar zijn. Deze mogelijkheid wordt in wezen maakt een kans tooselect bibliotheken en sjablonen maken voor verticale markten. Het is een belangrijk kenmerk van Azure Machine Learning op Hallo markt.  

We hopen dat toocontinue in dit onderwerp in Hallo toekomstige, met name gerelateerde toobig gegevensanalyse.
  

## <a name="conclusion"></a>Conclusie
Dit artikel beschrijft een verstandig tootackling Hallo veelvoorkomend probleem van klanten verloop met behulp van een algemene framework. We beschouwd als een prototype voor score berekenen voor modellen en geïmplementeerd met Azure Machine Learning. Ten slotte beoordeeld wij Hallo nauwkeurigheid en prestaties van Hallo prototype oplossing met inachtneming van toocomparable algoritmen in SAS.  

**Voor meer informatie:**  

Dit artikel kunt u? Geef ons uw feedback. Laat ons weten op een schaal van 1 (slecht) too5 (uitstekend), welke beoordeling zou u dit artikel worden en waarom hebt u het deze classificatie? Bijvoorbeeld:  

* Zijn u classificatie het hoge vervaldatum toohaving goede voorbeelden, uitstekende schermafdrukken, schakelt u schrijft, of een andere reden?
* Zijn u classificatie het lage vervaldatum toopoor voorbeelden, fuzzy schermopnamen of onduidelijk schrijven?  

Deze feedback helpt ons Hallo kwaliteit van whitepapers we brengen verbeteren.   

[Feedback verzenden](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Verwijzingen
[1] predictive Analytics: buiten Hallo-voorspellingen W. McKnight, informatiebeheer juli augustus 2011 p.18-20.  

[2] Wikipedia artikel: [nauwkeurigheid en juistheid](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [heldere-DM 1.0: stapsgewijze datamining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [big Data Marketing: uw klanten effectiever benaderen en waarde station](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Telco verloop model sjabloon](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Bijlage
![][10]

*Afbeelding 12: Momentopname van een prototype van de verloop-presentatie*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
