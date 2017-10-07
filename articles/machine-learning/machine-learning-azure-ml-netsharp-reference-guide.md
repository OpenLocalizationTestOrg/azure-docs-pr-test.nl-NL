---
title: 'aaaGuide toohello Net Neural Networks specificatietaal # | Microsoft Docs'
description: 'De syntaxis voor het Hallo Net # neural networks specificatietaal, samen met enkele voorbeelden van hoe toocreate aangepaste neurale netwerk wordt een model in Microsoft Azure ML met Net #'
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Handleiding tooNet neural network-specificatietaal # voor Azure Machine Learning
## <a name="overview"></a>Overzicht
NET # is een taal die is ontwikkeld door Microsoft dat gebruikte toodefine neural network-architecturen. U kunt Net # in neural network-modules in Microsoft Azure Machine Learning.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

In dit artikel leert u basisconcepten toodevelop neurale netwerk wordt een aangepaste nodig: 

* Vereisten voor neurale netwerk wordt en hoe toodefine Hallo primaire onderdelen
* Hallo-syntaxis en trefwoorden Hallo Net #-specificatietaal
* Voorbeelden van aangepaste neural netwerken die zijn gemaakt met Net # 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Basisprincipes van neurale netwerk
Een structuur neurale netwerk bestaat uit ***knooppunten*** die zijn ingedeeld in ***lagen***, en de gewogen ***verbindingen*** (of ***randen***) tussen Hallo-knooppunten. Hallo-verbindingen zijn gericht en elke verbinding heeft een ***bron*** knooppunt en een ***bestemming*** knooppunt.  

Elke ***trainable laag*** (een verborgen of een laag uitvoer) heeft een of meer ***verbinding bundels***. Een bundel verbinding bestaat uit een bronlaag en een specificatie van Hallo verbindingen van die bronlaag. Alle Hallo-verbindingen in een share opgegeven bundel Hallo dezelfde ***bronlaag*** en dezelfde Hallo ***bestemming laag***. In Net #, wordt beschouwd als een bundel verbinding als behoren toohello bundel bestemming laag.  

NET # ondersteunt verschillende soorten verbinding bundels, waarmee u Hallo manier invoer toegewezen toohidden lagen is aanpassen en toegewezen toohello levert.   

Hallo standaard of standaard bundel is een **volledige bundel**, in welke op elk knooppunt in Hallo bronlaag verbonden tooevery knooppunt in Hallo bestemming laag is.  

Daarnaast ondersteunt Net # Hallo vier soorten geavanceerde verbinding bundels te volgen:  

* **Gefilterd bundels**. Hallo-gebruiker kan een predikaat definiëren met behulp van Hallo locaties van de laag bronknooppunt Hallo en Hallo laag doelknooppunt. Knooppunten zijn verbonden wanneer Hallo predicaat True is.
* **Convolutional bundels**. Hallo-gebruiker kunt kleine groepen van knooppunten in Hallo bronlaag definiëren. Elk knooppunt in Hallo bestemming laag is verbonden tooone netwerkomgeving van knooppunten in Hallo bronlaag.
* **Groeperen van bundels** en **antwoord normalisatie bundels**. Dit zijn vergelijkbaar tooconvolutional bundels in die Hallo gebruiker kleine groepen van knooppunten in Hallo bronlaag definieert. Hallo verschil is dat er geen Hallo gewichten van Hallo randen in deze bundels trainable. In plaats daarvan een vooraf gedefinieerde functie wordt toegepast toohello bronknooppunt toodetermine Hallo bestemming knooppuntwaarde waarden.  

Met Net # maakt toodefine Hallo structuur van een neural netwerk het mogelijk toodefine complexe structuren zoals diep neural networks of convoluties van willekeurige dimensies, waarvan bekend is tooimprove leren op gegevens, zoals afbeelding, audio of video.  

## <a name="supported-customizations"></a>Ondersteunde aanpassingen
Hallo-architectuur van neural network-modellen die u in Azure Machine Learning maakt kan grote schaal worden aangepast via Net #. U kunt:  

* Verborgen lagen en besturingselement Hallo aantal knooppunten in elke laag maken.
* Geef op hoe lagen toobe verbonden tooeach, andere zijn.
* Speciale connectiviteit structuren, zoals convoluties en gewicht delen bundels definiëren.
* Geef de activering van andere functies.  

Zie voor meer informatie van Hallo specificatie syntaxis [structuur specificatie](#Structure-specifications).  

Zie voor voorbeelden van het definiëren van neural networks voor een aantal veelvoorkomende machine learning-taken uit simplex toocomplex [voorbeelden](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Algemene vereisten
* Moet er precies één uitvoer laag, ten minste één invoer-laag en nul of meer verborgen lagen. 
* Elke laag heeft een vast aantal knooppunten, conceptueel gerangschikt in een rechthoekige matrix met willekeurige dimensies. 
* Invoer lagen geen bijbehorende getraind parameters hebben en vertegenwoordigen Hallo punt waarbij exemplaargegevens Hallo netwerk invoert. 
* Trainable lagen (Hallo verborgen- en lagen) gekoppelde hebben getraind parameters, gewicht en vooroordelen genoemd. 
* Hallo-bron- en doelserver knooppunten moeten zich in verschillende lagen. 
* Verbindingen moet acyclische; Er kan niet met andere woorden, een keten van de initiële bronknooppunt back toohello voorloop-verbindingen.
* Hallo uitvoer laag kan niet een bronlaag van een bundel verbinding.  

## <a name="structure-specifications"></a>Structuur specificaties
Een structure-specificatie van het neurale netwerk bestaat uit drie secties: Hallo **constantendeclaratie**, Hallo **laag-declaratie**, Hallo **verbinding declaratie**. Er is ook een optionele **delen declaratie** sectie. Hallo secties kunnen in elke volgorde worden opgegeven.  

## <a name="constant-declaration"></a>Constantendeclaratie
Een constantendeclaratie is optioneel. Het biedt een manier toodefine waarden elders in de definitie van Hallo neurale netwerk wordt gebruikt. Hallo-declaratie-instructie bestaat uit een id die wordt gevolgd door een gelijkteken en een waardenexpressie.   

Hallo-instructie definieert u bijvoorbeeld een constante **x**:  

    Const X = 28;  

toodefine twee of meer constanten tegelijk, moet u Hallo-id-namen en waarden tussen accolades en gescheiden door puntkomma's. Bijvoorbeeld:  

    Const { X = 28; Y = 4; }  

Hallo rechterkant van de toewijzingsexpressie voor elke kan een geheel getal, een reëel getal, een Booleaanse waarde (True of False) of een rekenkundige expressie zijn. Bijvoorbeeld:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Laag-declaratie
Hallo laag declaratie is vereist. Het definieert Hallo-grootte en de bron van Hallo-laag, met inbegrip van de verbinding bundels en kenmerken. Hallo declaratie-instructie begint met de naam Hallo van Hallo-laag (invoer, verborgen of uitvoer), gevolgd door Hallo dimensies van Hallo-laag (een tuple van positieve gehele getallen). Bijvoorbeeld:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* Hallo product Hallo dimensies is het aantal knooppunten in de laag Hallo Hallo. In dit voorbeeld zijn er twee dimensies [5,20], wat betekent dat er 100 knooppunten in Hallo laag zijn.
* Hallo lagen kunnen worden gedeclareerd in willekeurige volgorde, met één uitzondering: Hallo volgorde waarin ze zijn gedeclareerd als meer dan één invoer laag is gedefinieerd, moet overeenkomen met Hallo volgorde van de functies in Hallo invoergegevens.  

toospecify dat het aantal knooppunten in een laag Hallo automatisch, gebruik Hallo bepaald **automatisch** sleutelwoord. Hallo **automatisch** sleutelwoord heeft verschillende effecten, afhankelijk van het Hallo-laag:  

* Hallo aantal knooppunten is in een declaratie invoer laag Hallo aantal functies in Hallo invoergegevens.
* In een declaratie verborgen laag Hallo van knooppunten Hallo getal is die is opgegeven door de parameterwaarde Hallo voor **aantal knooppunten dat verborgen**. 
* Hallo aantal knooppunten is in de declaratie van een uitvoer-laag 2 voor tweeklasse classificatie, 1 voor regressie en gelijk toohello aantal uitvoerknooppunten voor multiklassen classificatie.   

Hallo kan volgende netwerkdefinitie bijvoorbeeld Hallo grootte van alle lagen toobe automatisch bepaald:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


De declaratie van een laag voor een laag trainable (Hallo verborgen of uitvoergegevens lagen) kunt u eventueel Hallo uitvoer functie (ook wel een functie voor activering genoemd), die een te standaardwaarde opnemen**sigmoid** voor classificatie modellen en **lineaire** voor regressie-modellen. (Zelfs als u Hallo standaard gebruikt, u kunt expliciet aangeven Hallo activering functie, indien gewenst voor de duidelijkheid.)

Hallo worden volgende uitvoer functies ondersteund:  

* sigmoid
* Lineair
* softmax
* rlinear
* vierkante
* SQRT
* srlinear
* ABS
* TANH 
* brlinear  

Hallo declaratie volgende wordt bijvoorbeeld Hallo **softmax** functie:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Verbinding declaratie
Direct na het definiëren van Hallo trainable laag, moet u de verbindingen tussen Hallo lagen die u hebt gedefinieerd declareren. Hallo verbinding bundel declaratie begint met de Hallo sleutelwoord **van**, gevolgd door de naam van Hallo-bundel bron laag en Hallo soort verbinding bundel toocreate Hallo.   

Op dit moment worden verbinding bundels vijf typen ondersteund:  

* **Volledige** bundels, aangegeven door Hallo sleutelwoord **alle**
* **Gefilterd** bundels, aangegeven door Hallo sleutelwoord **waar**, gevolgd door een predikaat expressie
* **Convolutional** bundels, aangegeven door Hallo sleutelwoord **convolve**, gevolgd door Hallo convolutiefilter kenmerken
* **Groeperen van** bundels, aangegeven door Hallo trefwoorden **maximum aantal toepassingen** of **betekent dat de groep van toepassingen**
* **Antwoord normalisatie** bundels, aangegeven door Hallo sleutelwoord **antwoord norm**      

## <a name="full-bundles"></a>Volledige bundels
Een volledige verbinding bundel bevat een verbinding van elk knooppunt in Hallo laag tooeach bronknooppunt in Hallo bestemming laag. Dit is type netwerkverbinding Hallo standaard.  

## <a name="filtered-bundles"></a>Gefilterde bundels
Een gefilterde verbinding bundel specificatie bevat een veel-predicaat, syntaxis, uitgedrukt als een C# lambda-expressie. Hallo definieert volgende voorbeeld twee gefilterde bundels:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* In het Hallo-predicaat voor *ByRow*, **s** is een parameter die een index in Hallo rechthoekige matrix van knooppunten van de invoer laag hello, vertegenwoordigt *Pixels*, en **d**  is een parameter die een index in de matrix Hallo van knooppunten in de verborgen laag hello, vertegenwoordigt *ByRow*. type van beide Hallo **s** en **d** is een tuple van gehele getallen van twee lengte. Conceptueel gezien **s** bereiken via alle paren van gehele getallen met *0 < = s [0] < 10* en *0 < = s[1] < 20*, en **d**  bereiken via alle paren van gehele getallen, met *0 < = [0] d < 10* en *0 < = d[1] < 12*. 
* Aan de rechterkant Hallo van predicaatexpressie hello is er een voorwaarde. In dit voorbeeld wordt voor elke waarde van **s** en **d** zodat Hallo voorwaarde waar is, er is een rand van Hallo laag knooppunt toohello bestemming laag bronknooppunt. Dus deze filterexpressie aangeeft die bundel Hallo bevat een verbinding van het Hallo-knooppunt gedefinieerd door **s** toohello knooppunt gedefinieerd door **d** in alle gevallen waarbij s [0] gelijk tood [0] is.  

U kunt eventueel opgeven dat een set van gewicht voor een gefilterde bundel. waarde voor Hallo Hallo **gewichten** kenmerk moet een tuple met drijvende puntwaarden met een lengte die overeenkomt met het aantal verbindingen dat is gedefinieerd door Hallo bundel Hallo. Standaard worden gewichten willekeurig gegenereerd.  

Gewichtswaarden zijn gegroepeerd op Hallo bestemming knooppuntindex. Dat wil zeggen, als de eerste doelknooppunt Hallo is verbonden knooppunten van de bron, duurde eerst Hallo *K* elementen Hallo **gewichten** tuple Hallo gewichten voor Hallo eerste doelknooppunt, in volgorde van de index gegevensbron zijn. Hallo geldt ook voor Hallo resterende knooppunten van de bestemming.  

Het is mogelijk toospecify gewichten rechtstreeks als constante waarden. Bijvoorbeeld, als u Hallo gewichten eerder hebt geleerd, kunt u ze als constanten gebruik de volgende syntaxis:

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Convolutional bundels
Wanneer de trainingsgegevens Hallo een homogene structuur heeft, zijn convolutional verbindingen veelgebruikte toolearn op hoog niveau functies van Hallo-gegevens. Gegevens bijvoorbeeld: in afbeelding audio- of videobestanden, ruimtelijke of tijdelijke dimensionaliteit kunnen zijn redelijk uniform.  

Convolutional bundels alvast rechthoekige **kernels** die via Hallo dimensies worden geschoven. In wezen elke kernel definieert een reeks gewichten toegepast in de lokale groepen, waarnaar wordt verwezen tooas **kerneltoepassingen**. Elke toepassing kernel overeenkomt met tooa-knooppunt in Hallo bronlaag, die bedoeld tooas hello is **centrale knooppunt**. Hallo-gewicht van een kernel worden gedeeld door veel verbindingen. In een convolutional bundel elke kernel rechthoekige en alle kerneltoepassingen Hallo dezelfde grootte.  

Convolutional bundels ondersteunen Hallo volgende kenmerken:

**InputShape** Hallo dimensionaliteit van Hallo bronlaag voor de toepassing hello van deze convolutional bundel definieert. Hallo-waarde moet een tuple van positieve gehele getallen zijn. Hallo product van gehele getallen Hallo moet gelijk zijn aan het aantal knooppunten in Hallo bronlaag Hallo maar anders hoeft niet toomatch Hallo dimensionaliteit gedeclareerd voor Hallo bronlaag. Hallo-lengte van deze tuple wordt Hallo **ariteit** waarde voor Hallo convolutional bundel. (De ariteit verwijst doorgaans toohello aantal argumenten of operanden die kan worden uitgevoerd door een functie.)  

toodefine hello vorm en de locaties van Hallo-kernels Hallo kenmerken gebruiken **KernelShape**, **Stride**, **opvulling**, **LowerPad**, en **UpperPad**:   

* **KernelShape**: (vereist) definieert Hallo dimensionaliteit van elke kernel voor Hallo convolutional bundel. Hallo-waarde moet een tuple van positieve gehele getallen met een lengte die gelijk is aan Hallo ariteit van Hallo-bundel. Elk onderdeel van deze tuple mag niet langer zijn dan het overeenkomstige onderdeel Hallo van **InputShape**. 
* **Stride**: (optioneel) definieert Hallo Verschuivend stap grootten van Hallo convolutiefilter (één stapgrootte voor elke dimensie), die is Hallo afstand tussen Hallo centrale knooppunten. Hallo-waarde moet een tuple van positieve gehele getallen met een lengte die Hallo ariteit van Hallo-bundel. Elk onderdeel van deze tuple mag niet langer zijn dan het overeenkomstige onderdeel Hallo van **KernelShape**. Hallo-standaardwaarde is een tuple met alle onderdelen gelijk tooone. 
* **Delen**: (optioneel) definieert Hallo gewicht voor elke dimensie van Hallo convolutiefilter delen. Hallo-waarden zijn één Booleaanse waarde of een tuple van Booleaanse waarden met een lengte die Hallo ariteit van Hallo-bundel. Een enkele Booleaanse waarde is een tuple van de juiste lengte Hallo met alle onderdelen van uitgebreide toobe gelijk toohello opgegeven waarde. Hallo-standaardwaarde is een tuple die uit alle waar waarden bestaat. 
* **MapCount**: (optioneel) definieert Hallo aantal functie voor Hallo convolutional bundel wordt toegewezen. Hallo-waarde is een enkel positief geheel getal of een tuple van positieve gehele getallen met een lengte die Hallo ariteit van Hallo-bundel. Een enkele geheelgetalwaarde wordt uitgebreid toobe een tuple van de juiste lengte Hallo met Hallo eerste onderdelen gelijk toohello opgegeven waarde en alle overige onderdelen gelijk tooone Hallo. Hallo-standaardwaarde is een. Totaal aantal functie maps Hallo is Hallo product van Hallo onderdelen van Hallo tuple. Hallo waarbij van dit totale aantal voor Hallo onderdelen bepaalt hoe Hallo functie kaart waarden worden gegroepeerd in Hallo bestemming knooppunten. 
* **Gewicht**: (optioneel) definieert Hallo initiële gewichten voor Hallo bundel. Hallo-waarde moet een tuple met drijvende puntwaarden met een lengte die Hallo aantal kernels keer Hallo aantal gewichten per kernel, zoals verderop in dit artikel is gedefinieerd. Hallo standaardgewichten worden willekeurig gegenereerd.  

Er zijn twee sets van eigenschappen die regelen opvulling, Hallo eigenschappen wordt sluiten elkaar wederzijds uit:

* **Opvulling**: (optioneel) bepaalt of Hallo invoer moet zijn opgevuld met behulp van een **opvulling standaardschema**. Hallo-waarde kan één Booleaanse waarde, of het kan ook een tuple van Booleaanse waarden met een lengte die Hallo ariteit van Hallo-bundel. Een enkele Booleaanse waarde is een tuple van de juiste lengte Hallo met alle onderdelen van uitgebreide toobe gelijk toohello opgegeven waarde. Als de waarde voor een dimensie Hallo True is, worden Hallo bron logisch opgevuld in die dimensie met cellen nul met toosupport extra kerneltoepassingen dat Hallo centrale knooppunten van de eerste en laatste kernels Hallo in die dimensie Hallo eerste en laatste knooppunten worden in die dimensie in Hallo bronlaag. Hallo aantal 'dummy' knooppunten in elke dimensie is dus automatisch bepaald, toofit exact *(InputShape [d] - 1) / Stride [d] + 1* kernels in Hallo opgevuld bronlaag. Als de waarde voor een dimensie Hallo False is, Hallo Hallo kernels zijn gedefinieerd, zodat het aantal knooppunten voor elke zijde die worden weggelaten Hallo is dezelfde (omhoog tooa verschil van 1). de standaardwaarde Hallo van dit kenmerk is een tuple met alle onderdelen gelijk tooFalse.
* **UpperPad** en **LowerPad**: (optioneel) Geef meer controle over de hoeveelheid opvulling toouse Hallo. **Belangrijk:** deze kenmerken kunnen worden gedefinieerd als en alleen als hello **opvulling** eigenschap hierboven is ***niet*** gedefinieerd. Hallo-waarden moet geheel getalwaarde tuples met een lengte die Hallo ariteit van Hallo-bundel. Deze kenmerken worden opgegeven, 'dummy' knooppunten toohello lagere worden toegevoegd als bovenste ends van iedere dimensie van Hallo invoer laag. Hallo aantal knooppunten toegevoegd toohello lagere en bovenste eindigt in elke dimensie wordt bepaald door **LowerPad**[i] en **UpperPad**[i] respectievelijk. tooensure dat kernels overeenkomen alleen te 'echte' knooppunten en knooppunten niet te 'dummy' hello volgende voorwaarden is voldaan:
  * Elk onderdeel van **LowerPad** moet strikt kleiner zijn dan KernelShape [d] / 2. 
  * Elk onderdeel van **UpperPad** mag niet langer zijn dan KernelShape [d] / 2. 
  * Hallo-standaardwaarde van deze kenmerken is een tuple met alle onderdelen gelijk too0. 

Hallo-instelling **opvulling** = true kan zo veel opvulling omdat tookeep Hallo "center" van de kernel Hallo binnen Hallo 'echte' invoer nodig. Hiermee wijzigt u Hallo math iets voor computergebruik Hallo uitvoergrootte. In het algemeen Hallo grootte uitvoer *D* wordt berekend als *D = (I - K) / S + 1*, waarbij *ik* invoergrootte hello, is *K* is Hallo kernel omvang *S* Hallo-stride is en  */*  deling van geheel getal (afronden op nul) is. Als u UpperPad instellen = [1, 1], Hallo invoer grootte *ik* is in feite 29, en dus *D = (29-5) / 2 + 1 = 13*. Echter, wanneer **opvulling** = true, wordt in wezen *ik* opgehaald tegenaan door *K - 1*; daarom *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. Door op te geven waarden voor **UpperPad** en **LowerPad** dat u veel meer controle over Hallo opvulling dan als u zojuist hebt ingesteld **opvulling** = true.

Zie voor meer informatie over convolutional netwerken en hun toepassingen in deze artikelen:  

* [http://deeplearning.NET/Tutorial/lenet.HTML](http://deeplearning.net/tutorial/lenet.html)
* [http://Research.Microsoft.com/pubs/68920/icdar03.PDF](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://People.csail.MIT.edu/jvb/Papers/cnn_tutorial.PDF](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Bundels groeperen
A **groeperen bundel** geldt geometrie vergelijkbare tooconvolutional connectiviteit, maar het vooraf gedefinieerde functies toosource waarden tooderive Hallo bestemming knooppunt knooppuntwaarde gebruikt. Groepering bundels hebben daarom geen trainable status (gewichten of vooroordelen). Groeperen bundels ondersteuning alle convolutional kenmerken behalve Hallo **delen**, **MapCount**, en **gewichten**.  

Normaal gesproken overlappen Hallo kernels samengevat door aangrenzende groepering eenheden niet. Als Stride [d] gelijk tooKernelShape [d] in elke dimensie is, is Hallo laag verkregen Hallo traditionele lokale groepering laag, die meestal in convolutional neural netwerken gebruikt wordt. Elke doelknooppunt berekent Hallo maximale of Hallo gemiddelde van Hallo activiteiten van de kernel in Hallo bronlaag.  

Hallo volgende voorbeeld ziet u een groepering bundel: 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* Hallo ariteit van Hallo-bundel is 3 (lengte van Hallo tuples Hallo **InputShape**, **KernelShape**, en **Stride**). 
* het aantal knooppunten in Hallo bronlaag Hallo is *5 * 24 * 24 = 2880*. 
* Dit is een traditionele lokale groepering laag omdat **KernelShape** en **Stride** gelijk zijn. 
* het aantal knooppunten in Hallo bestemming laag Hallo is *5 * 12 * 12 = 1440*.  

Zie voor meer informatie over groepering lagen deze artikelen:  

* [http://www.cs.Toronto.edu/~hinton/absps/imagenet.PDF](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (sectie 3.4)
* [http://CS.Nyu.edu/~koray/publis/lecun-iscas-10.PDF](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://CS.Nyu.edu/~koray/publis/jarrett-iccv-09.PDF](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Antwoord normalisatie bundels
**Antwoord normalisatie** is een lokale normalisatie-schema dat is geïntroduceerd door Geoffrey Hinton, et al. in Hallo artikel [ImageNet Classiﬁcation met Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Antwoord normalisatie is gebruikte tooaid generaliseren van neural netten. Wanneer een neuron wordt uitgevoerd op een zeer hoge Activeringsniveau, onderdrukt een lokale antwoord normalisatie-laag Hallo Activeringsniveau Hallo omringende neurons. Dit wordt gedaan met drie parameters (***α***, ***β***, en ***k***) en een convolutional structuur (of groep vorm). Elke neuron in Hallo bestemming laag ***y*** overeenkomt met tooa neuron ***x*** in Hallo bronlaag. Activeringsniveau van Hallo ***y*** wordt bepaald door de volgende formule, Hallo waar ***f*** Hallo activering niveau van een neuron en ***Nx*** kernel hello (of Hallo set met Hallo neurons in de groep Hallo van ***x***), zoals gedefinieerd door Hallo convolutional structuur te volgen:  

![][1]  

Antwoord normalisatie bundels ondersteuning voor alle Hallo convolutional kenmerken behalve **delen**, **MapCount**, en **gewichten**.  

* Als de kernel Hallo neurons in Hallo bevat dezelfde toewijzen als ***x***, Hallo normalisatie-schema is waarnaar wordt verwezen tooas **dezelfde normalisatie toewijzen**. toodefine dezelfde toewijzen normalisatie wordt de eerste coördinaat Hallo in **InputShape** moet Hallo waarde 1 hebben.
* Als Hallo kernel neurons in Hallo bevat dezelfde ruimtelijke positie als ***x***, maar Hallo neurons zijn in andere toewijzingen, Hallo normalisatie schema heet **meerdere toegewezen normalisatie**. Dit type antwoord normalisatie implementeert een vorm van laterale maar die is geïnspireerd op Hallo type gevonden in de echte neurons concurrentie voor big activering niveaus onder neuron uitvoer berekend op verschillende maps maken. toodefine over normalisatie wordt toegewezen, Hallo eerste coördinaat moet een geheel getal groter dan één en niet groter zijn dan het aantal maps Hallo en rest Hallo Hallo coördinaten moet Hallo waarde 1 hebben.  

Omdat het antwoord normalisatie bundels een vooraf gedefinieerde functie toosource knooppunt waarden toodetermine Hallo bestemming knooppuntwaarde toegepast, hebben ze geen trainable status (gewichten of vooroordelen).   

**Waarschuwing**: Hallo knooppunten in Hallo bestemming laag tooneurons die Hallo centrale knooppunten van Hallo kernels overeenkomen. Bijvoorbeeld, als KernelShape [d] oneven en wordt vervolgens *KernelShape [d] / 2* overeenkomt met toohello centrale kernel-knooppunt. Als *KernelShape [d]* een even getal is, Hallo centrale knooppunt loopt *KernelShape [d] / 2-1*. Daarom als **opvulling**[d] is ingesteld op False, Hallo het eerste en laatste Hallo *KernelShape [d] / 2* knooppunten hebben geen overeenkomstige knooppunten in Hallo bestemming laag. tooavoid deze situatie definiëren **opvulling** als [true, true,..., true].  

Bovendien toohello vier kenmerken die eerder zijn beschreven, antwoord normalisatie bundels ook ondersteuning Hallo volgende kenmerken:  

* **Alpha**: (vereist) geeft een drijvende-kommawaarde die overeenkomt met te***α*** in de vorige formule Hallo. 
* **Beta**: (vereist) geeft een drijvende-kommawaarde die overeenkomt met te***β*** in de vorige formule Hallo. 
* **Offset**: (optioneel) geeft een drijvende-kommawaarde die overeenkomt met te***k*** in de vorige formule Hallo. De standaardwaarde too1.  

Hallo definieert volgende voorbeeld een antwoord normalisatie-bundel met behulp van deze kenmerken:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* Hallo bronlaag bevat vijf maps, elk met aof dimensie van 12 x 12 Samentelling in 1440 knooppunten. 
* waarde van Hallo **KernelShape** geeft aan dat dit een dezelfde normalisatie kaartLaag, waarbij Hallo groep een rechthoek 3 x 3 is. 
* Hallo standaardwaarde van **opvulling** is ingesteld op False, Hallo bestemming laag heeft dus alleen 10 knooppunten in elke dimensie. een knooppunt in Hallo bestemming laag die overeenkomt met tooevery-knooppunt in Hallo bronlaag toevoegen opvulling tooinclude = [true, true, true]; en Hallo grootte van RN1 te wijzigen [5, 12, 12].  

## <a name="share-declaration"></a>Share-declaratie
NET # ondersteunt eventueel meerdere pakketten met gedeelde gewichten definiëren. Hallo-gewicht van elke twee bundels kunnen worden gedeeld als hun structuren zijn dezelfde Hallo. de volgende syntaxis Hallo definieert bundels met gedeelde gewichten:  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Hallo geeft volgende share-declaratie bijvoorbeeld Hallo laagnamen, die aangeeft dat de gewichten en vooroordelen worden gedeeld:  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* Hallo invoer functies worden gepartitioneerd in twee gelijke grootte invoer lagen. 
* Hallo verborgen lagen berekent hoger niveau functies op Hallo van de twee ingevoerde lagen. 
* Hallo-share-declaratie geeft aan dat *H1* en *H2* moet worden berekend in Hallo dezelfde manier uit hun respectieve invoer.  

U kunt ook kan dit worden opgegeven met twee afzonderlijke share-declaraties als volgt:  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

U kunt Hallo verkorte vorm alleen als Hallo lagen één bundel bevatten. In het algemeen is delen mogelijk alleen als de relevante Hallo-structuur identiek zijn, zodat ze Hallo dezelfde grootte, dezelfde convolutional geometrie, enzovoort.  

## <a name="examples-of-net-usage"></a>Voorbeelden van Net # gebruik
Deze sectie vindt u enkele voorbeelden van hoe kunt u Net # tooadd verborgen lagen, Hallo manier verborgen lagen communiceren met andere lagen en bouwen van netwerken convolutional definiëren.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Een eenvoudig aangepaste neurale netwerk definiëren: 'Hallo wereld'-voorbeeld
Dit eenvoudige voorbeeld laat zien hoe toocreate een neural network model met één laag verborgen.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

Hallo-voorbeeld wordt door sommige basisopdrachten als volgt:  

* Hallo eerste regel definieert Hallo invoer laag (met de naam *gegevens*). Wanneer u Hallo gebruikt **automatisch** trefwoord Hallo neurale netwerk omvat alle kolommen van de functie automatisch in Hallo invoer voorbeelden. 
* de tweede regel Hallo maakt Hallo verborgen laag. de naam van de Hallo *H* toohello verborgen laag, die 200 knooppunten heeft is toegewezen. Deze laag is volledig verbonden toohello invoer laag.
* de derde regel Hallo definieert Hallo uitvoer laag (met de naam *O*), die 10 uitvoerknooppunten bevat. Als Hallo neurale netwerk wordt gebruikt voor classificatie, is er één knooppunt van de uitvoer per klasse. Hallo sleutelwoord **sigmoid** geeft aan dat het Hallo uitvoer functie toegepaste toohello uitvoer laag.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Meerdere verborgen lagen definiëren: computer vision-voorbeeld
Hallo volgende voorbeeld laat zien hoe toodefine iets meer complexe neurale netwerk, met meerdere lagen voor aangepaste verborgen.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

In dit voorbeeld ziet u diverse functies van Hallo neural networks specificatietaal:  

* Hallo-structuur heeft twee invoer lagen, *Pixels* en *metagegevens*.
* Hallo *Pixels* laag is een bronlaag voor twee verbinding-bundels met lagen van de bestemming, *ByRow* en *ByCol*.
* Hallo lagen *verzamelen* en *resultaat* bestemming lagen in meerdere pakketten van de verbinding zijn.
* Hallo uitvoer laag *resultaat*, is een doellaag in twee verbinding bundels; één Hello tweede niveau verborgen (verzamelen) als een doellaag en andere met invoer Hallo-laag (metagegevens) als een laag bestemming Hallo.
* verborgen lagen Hallo *ByRow* en *ByCol*, gefilterde verbinding opgeven met behulp van predikaat expressies. Preciezer, Hallo knooppunt in *ByRow* op [x, y] is verbonden toohello knooppunten in *Pixels* waarvoor de eerste coördinaat, x Hallo eerste index coördinaat gelijk toohello van het knooppunt. Op deze manier Hallo knooppunt in *ByCol op [x, y] is verbonden toohello knooppunten in _Pixels* waarvoor Hallo tweede index coördinaat binnen één van de tweede coördinaat van het knooppunt hello, y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Definieer een convolutional netwerk voor multiklassen classificatie: cijfer erkenning voorbeeld
Hallo definitie van de volgende netwerk Hallo is ontworpen toorecognize getallen en sommige geavanceerde technieken voor het aanpassen van een neural netwerk worden geïllustreerd.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* Hallo-structuur heeft één invoer laag *installatiekopie*.
* Hallo sleutelwoord **convolve** geeft aan dat de Hallo lagen naam *Conv1* en *Conv2* convolutional lagen. Elk van deze laag declaraties wordt gevolgd door een lijst met Hallo convolutiefilter kenmerken.
* Hallo net is een derde verborgen laag *Hid3*, toohello tweede verborgen laag, die volledig is verbonden *Conv2*.
* Hallo uitvoer laag *cijfer*, is verbonden alleen toohello derde verborgen laag, *Hid3*. Hallo sleutelwoord **alle** die laag Hallo-uitvoer is volledig te verbonden*Hid3*.
* Hallo ariteit van Hallo convolutiefilter is drie (lengte van Hallo tuples Hallo **InputShape**, **KernelShape**, **Stride**, en **delen**). 
* Hallo aantal gewichten per kernel is *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26. Of 26 * 50 = 1300*.
* U kunt als volgt Hallo knooppunten in de verborgen laag berekenen:
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13-5) / 2 + 1 = 5. 
  * **NodeCount**\[2] (13-5) = / 2 + 1 = 5. 
* Hallo totale aantal knooppunten kan worden berekend met behulp van Hallo gedeclareerd dimensionaliteit Hallo layer, [50, 5, 5], als volgt:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* Omdat **delen**[d] False is alleen voor *d == 0*, is het aantal kernels Hallo  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Bevestigingen
Hallo Net # taal voor het aanpassen van Hallo-architectuur van neural networks is bij Microsoft ontwikkeld door Shon Katzenberger (Architect, Machine Learning) en Alexey Kamenev (Software Engineer, Microsoft Research). Het wordt intern gebruikt voor machine learning-projecten en toepassingen, variërend van afbeelding detectie tootext analytics. Zie voor meer informatie [Neural netten in Azure ML - inleiding tooNet #](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

