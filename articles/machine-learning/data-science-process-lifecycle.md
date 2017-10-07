---
title: aaaAzure Team gegevens wetenschap proces Lifecycle | Microsoft Docs
description: Stappen nodig tooexecute projecten wetenschappelijke gegevens.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Levenscyclus van de procedure voor het wetenschappelijke gegevens team

Hallo Team gegevens wetenschap proces (TDSP) biedt een aanbevolen lifecycle waarmee u toostructure projecten wetenschappelijke gegevens kunt. Hallo lifecycle bevat een overzicht van Hallo stappen van de start-toofinish die projecten meestal volgt wanneer ze worden uitgevoerd. Als u een andere gegevens wetenschappelijke levensduur, zoals gebruikt [heldere DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) of uw organisatie zelf aangepast proces, kunt u Hallo TDSP op basis van een taak met deze levenscycli van de ontwikkeling. 

Deze levenscyclus beheren is ontworpen voor gegevens wetenschappelijke projecten die beoogde tooship als onderdeel van intelligente toepassingen. Deze toepassingen implementeren machine learning of kunstmatige intelligence modellen voor predictive analytics. Experimentele gegevens wetenschappelijke projecten en ad-hoc analytics projecten kunnen ook profiteren van dit proces. Maar in dergelijke gevallen mogelijk niet sommige stappen nodig.    

Hier volgt een visuele representatie van Hallo **Team gegevens wetenschap proces lifecycle**. 

![Levenscyclus van TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Hallo TDSP lifecycle bestaat uit vijf belangrijke fasen die iteratief worden uitgevoerd. Deze omvatten:

* **Wat voor bedrijven**
* **Gegevensverzameling en begrijpen**
* **Modeling**
* **Implementatie**
* **Acceptatie van de klant**

Voor elke fase bieden we Hallo volgende informatie:

* **Doelstellingen**: Hallo specifieke doelstellingen.
* **Hoe toodo het**: Hallo specifieke taken die worden beschreven en richtlijnen voor het voltooien van deze.
* **Artefacten**: Hallo-producten en Hallo bieden ondersteuning voor productie.


## <a name="1-business-understanding"></a>1. Inzicht in het bedrijf

### <a name="goals"></a>Doelstellingen
* Hallo **sleutel variabelen** zijn opgegeven die zijn tooserve als Hallo **model doelen** en waarvan verwante metrische gegevens worden gebruikt Hallo is geslaagd voor Hallo project bepalen.
* Hallo relevante **gegevensbronnen** worden geïdentificeerd dat Hallo bedrijven toegang tooor behoeften tooobtain heeft.

### <a name="how-toodo-it"></a>Hoe toodo deze
Er zijn twee belangrijke taken in deze fase verholpen: 

* **Definieer de doelstellingen van**: werken met uw klant en andere betrokkenen toounderstand en Hallo zakelijke problemen te identificeren. Vragen die Hallo zakelijke doelstellingen en dat de gegevens wetenschappelijke technieken kunnen richten definiëren formuleren.
* **Identificeren van gegevensbronnen**: zoeken Hallo relevante gegevens die u helpt vragen Hallo die Hallo doelstellingen van Hallo project definiëren.

#### <a name="11-define-objectives"></a>1.1 doelstellingen definiëren

1. Een centrale doel van deze stap is het tooidentify Hallo sleutel **business variabelen** dat Hallo analysis toopredict nodig. Deze variabelen zijn waarnaar wordt verwezen tooas hello **model doelen** en Hallo metrische gegevens die zijn gekoppeld aan deze gebruikte toodetermine Hallo succes van Hallo project zijn. Twee voorbeelden van dergelijke doelen zijn verkoop prognose of Hallo waarschijnlijkheid van een order fraude.

2. Hallo definiëren **doelstellingen project** door te vragen en '-kruis' vragen die betrokken en niet-ambigue zijn verfijnen. Gegevenswetenschap is Hallo proces van het gebruik van namen en getallen tooanswer dergelijke vragen. Zie voor meer informatie over het kruis vragen [hoe toodo Gegevenswetenschap](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/) blog. Gegevenswetenschap-machine learning is gewoonlijk gebruikte tooanswer vijf typen vragen:
 
   * Hoeveel of hoeveel? (regressie)
   * Welke categorie? (indeling)
   * Welke groep? (clustering)
   * Is dit vreemd? (afwijkingsdetectie)
   * Welke optie moet worden gehouden? (aanbevolen)

    Bepalen welke van deze vragen u vragen en hoe beantwoorden bereikt uw bedrijfsdoelen.

3. Hallo definiëren **project team** door te geven Hallo rollen en verantwoordelijkheden van de bijbehorende leden. Ontwikkel een belangrijke mijlpaalplan dat u herhalen als u meer informatie wordt gedetecteerd.  

4. **Maatstaven voor succes definiëren**. Voorbeeld: klant verloop nauwkeurigheid van X % bereiken door Hallo einde van dit project 3 maanden zodat we promoties tooreduce verloop bieden. Hallo metrische gegevens moet **SMART**: 
   * **S**pecifieke 
   * **M**easurable
   * **Een**chievable 
   * **R**elevant 
   * **T**ime-gebonden 

#### <a name="12-identify-data-sources"></a>1.2 gegevensbronnen identificeren
Identificeer de gegevensbronnen die bekende voorbeelden van antwoorden tooyour kruis vragen bevatten. Hallo volgt gegevens zoeken:

* De gegevens die zijn **relevante** toohello vraag. Hebben we metingen van Hallo doel en functies die gerelateerd toohello doel zijn?
* Gegevens die een **nauwkeurige weerspiegeling** van onze model doel en Hallo-functies van belang.

Het is niet ongewoon, bijvoorbeeld toofind die bestaande systemen toocollect nodig hebt en meld u aanvullende soorten gegevens tooaddress probleem Hallo en Hallo projectdoelstellingen te bereiken. U kunt in dit geval wilt toolook voor externe gegevensbronnen of bijwerken van uw systemen toocollect nieuwe gegevens.

### <a name="artifacts"></a>Artefacten
Hier volgen Hallo producten in deze fase:

* [**Document huren**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): een standaardsjabloon in Hallo TDSP project structuurdefinitie is opgegeven. Dit is een levende-document dat is bijgewerkt voor de gehele Hallo project als nieuwe detecties zijn aangebracht en als zakelijke vereisten veranderen. Hallo-sleutel is tooiterate bij dit document nader bekijken, toe te voegen bij het detectieproces Hallo. Houd Hallo klant en andere betrokkenen betrokken bij Hallo wijzigingen aanbrengen en duidelijk communiceren Hallo Hallo wijzigingen toothem redenen.  
* [**Gegevensbronnen**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): dit is Hallo **onbewerkte gegevensbronnen** sectie Hallo **gegevensdefinities** rapport dat is gevonden in Hallo TDSP project **rapport**  map. Het bevat oorspronkelijke hello- en doellocaties voor Hallo onbewerkte gegevens. In latere fasen verlopen, moet u extra details, zoals scripts toomove Hallo gegevens tooyour analytische omgeving invullen.  
* [**Gegevens woordenlijsten**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries): dit document vindt u beschrijvingen van Hallo-gegevens die door Hallo-client wordt geleverd. Deze beschrijvingen bevatten informatie over het Hallo-schema (gegevenstypen, informatie over validatieregels, indien van toepassing) en entiteit relatie diagrammen Hallo indien beschikbaar.


## <a name="2-data-acquisition-and-understanding"></a>2. Gegevens verzamelen en begrijpen

### <a name="goals"></a>Doelstellingen
* Een schone, hoogwaardige gegevensset waarvan relaties toohello target-variabelen te begrijpen die zich bevinden in Hallo juiste analytics-omgeving gereed toomodel.
* De oplossingsarchitectuur van een van Hallo data pipeline toorefresh en score gegevens regelmatig is ontwikkeld.

### <a name="how-toodo-it"></a>Hoe toodo deze
Er zijn drie belangrijkste taken in deze fase behandeld:

* **Hallo gegevens opnemen** in analytische doelomgeving Hallo.
* **Hallo-gegevens verkennen** toodetermine als Hallo gegevenskwaliteit voldoende tooanswer Hallo vraag is. 
* **Instellen van een pijplijn gegevens** tooscore nieuw of regelmatig vernieuwd gegevens.

#### <a name="21-ingest-hello-data"></a>2.1 Hallo gegevens opnemen
Hallo proces toomove Hallo gegevens instellen van bronlocaties toohello doellocaties waarin analytics-bewerkingen, zoals training en voorspellingen zijn toobe uitgevoerd. Voor technische informatie en -opties op hoe toodo met verschillende Azure data services, Zie [gegevens laden in omgevingen met opslag voor analyses](machine-learning-data-science-ingest-data.md). 

#### <a name="22-explore-hello-data"></a>2.2 Hallo gegevens verkennen
Voordat u uw modellen trainen, moet u toodevelop een goed begrip van Hallo-gegevens. Echte gegevenssets zijn vaak veel ruis veroorzaken of ontbreken waarden hebben tal van andere verschillen. Gegevenssamenvatting en visualisatie kunnen gebruikte tooaudit Hallo kwaliteit van uw gegevens en Hallo informatie nodig tooprocess Hallo gegevens voordat deze gereed voor het model is. Dit proces worden vaak herhaald.

TDSP biedt een geautomatiseerde hulpprogramma genaamd [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp Hallo gegevens visualiseren en bereid Samenvattingsrapporten van gegevens. Het is raadzaam beginnen met IDEAR eerste tooexplore Hallo gegevens toohelp initiële gegevens beter te leren kennen interactief met geen coderen en vervolgens aangepaste code schrijven voor gegevensverkenning en visualisatie. Zie voor instructies over het opruimen van Hallo gegevens [tooprepare taakgegevens voor verbeterde machine learning](machine-learning-data-science-prepare-data.md).  

Wanneer u tevreden met Hallo kwaliteit van Hallo gereinigd gegevens bent, de volgende stap Hallo toobetter is begrijpen Hallo patronen met zich mee Hallo-gegevens die u helpen kiezen en ontwikkelen van een juiste Voorspellend model voor uw doel. Let erop dat voor hoe goed verbonden Hallo gegevens toohello doel is en of er voldoende gegevens toomove doorsturen met Hallo volgende modellering stappen. Dit proces is opnieuw vaak herhaald. Mogelijk moet u de nieuwe gegevensbronnen toofind met nauwkeuriger of meer relevante gegevens tooaugment Hallo dataset aangegeven in de vorige fase Hallo.  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 instellen van een pijplijn gegevens
Bovendien Hallo toohello initiële opname en schoonmaken van gegevens, doorgaans moet u tooset een proces tooscore nieuwe gegevens of gegevens van de Hallo vernieuwen regelmatig als onderdeel van een doorlopende leerproces. Dit kan worden gedaan door het instellen van een pijplijn gegevens of de werkstroom. Hier volgt een [voorbeeld](machine-learning-data-science-move-sql-azure-adf.md) van hoe tooset van een pijplijn met [Azure Data Factory](https://azure.microsoft.com/services/data-factory/). 

De oplossingsarchitectuur van een van Hallo gegevens pijplijn is ontwikkeld in deze fase. Hallo-pijplijn wordt ook in combinatie met de volgende stadia van Hallo gegevens wetenschappelijke project Hallo ontwikkeld. Hallo pijplijn kan op basis van een batch of streaming/real-eenmalig of een hybride, afhankelijk van uw bedrijf moet en Hallo beperkingen van uw bestaande systemen waarin deze oplossing wordt geïntegreerd. 

### <a name="artifacts"></a>Artefacten
Hallo volgen Hallo producten in deze fase.

* [**Rapport met inventarisatiegegevens kwaliteit**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md): dit rapport bevat gegevens samenvattingen van de relaties tussen elk kenmerk en doel, enzovoort Hallo rangschikking variabele [IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) hulpprogramma dat is opgegeven als onderdeel van TDSP snel kunt genereren Dit rapport voor een tabellarische gegevensset zoals een CSV-bestand of een relationele tabel. 
* **Oplossingsarchitectuur**: dit kan een diagram of beschrijving van uw gegevens pijplijn gebruikt toorun score berekenen of voorspellingen op nieuwe gegevens zijn wanneer u een model hebt gebouwd. Het bevat ook Hallo pijplijn tooretrain uw model op basis van nieuwe gegevens. Hallo-document is opgeslagen in Hallo [Project](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project) directory wanneer u de sjabloon Hallo TDSP directory-structuur.
* **Controlepunt besluit**: voordat u volledige functie-engineering en model bouwen, kunt u Hallo project toodetermine Herzie of verwachte Hallo-waarde is voldoende toocontinue deze in het kader. U kunt bijvoorbeeld wel gereed tooproceed, moeten toocollect worden meer gegevens of afbreken Hallo project als Hallo gegevens tooanswer Hallo vraag niet bestaat..


## <a name="3-modeling"></a>3. Modelleren

### <a name="goals"></a>Doelstellingen
* De functies van de optimale gegevens voor Hallo machine learning-model.
* Een informatieve ML-model dat Hallo doel nauwkeurigst voorspelt.
* Een ML-model dat geschikt is voor productie.

### <a name="how-toodo-it"></a>Hoe toodo deze
Er zijn drie belangrijkste taken in deze fase behandeld:

* **Functie-Engineering**: gegevensfuncties van Hallo onbewerkte gegevens toofacilitate model training maken.
* **Training model**: Hallo model vinden die antwoorden Hallo vraag nauwkeurigst door hun maatstaven voor succes vergelijken.
* Bepalen of uw model **geschikt is voor productie**.

#### <a name="31-feature-engineering"></a>3.1 functie-engineering
Functie-engineering omvat insluiting, aggregatie en transformatie van onbewerkte variabelen toocreate Hallo functies die worden gebruikt in Hallo analyse. Als u inzicht in wat een model wordt bestuurd wilt, moet u toounderstand hoe functies andere gerelateerde tooeach zijn en hoe Hallo machine learning-algoritmen toouse zijn deze functies. Deze stap moet u een creative combinatie van expertise in verschillende domeinen en inzichten die zijn verkregen via Hallo gegevens verkenning stap. Dit is een evenwichtsoefening van zoeken en informatieve variabelen vermeden te veel niet-verwante variabelen, inclusief. Informatieve variabelen verbeteren van onze resultaat; niet-verwante variabelen introduceren onnodige ' ruis ' in hello model. U moet ook toogenerate deze functies voor alle nieuwe gegevens die zijn verkregen tijdens het berekenen van de score. Hallo generatie van deze functies kan dus alleen afhankelijk zijn van gegevens die beschikbaar is op Hallo moment score berekenen. Zie voor technische richtlijnen op functie-engineering bij gebruik van verschillende technologieën van Azure data [functie-engineering in Hallo gegevens wetenschap proces](machine-learning-data-science-create-features.md). 

#### <a name="32-model-training"></a>3.2 modeltraining
Afhankelijk van het type dat u antwoord probeert vraag, zijn er veel modellering algoritmen beschikbaar. Zie voor instructies over het kiezen van Hallo algoritmen [hoe toochoose algoritmen voor Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md). Hoewel dit artikel is geschreven voor Azure Machine Learning, Hallo richtlijnen biedt is handig voor een machine learning-projecten. 

Hallo-proces voor het model trainen bevat Hallo stappen te volgen: 

* **Gesplitste Hallo invoergegevens** willekeurig voor modellen in een set trainingsgegevens en een test-gegevensset.
* **Hallo modellen bouwen** set trainingsgegevens hello gebruiken.
* **Evalueren** (trainings- en testset gegevensset) een reeks concurrerende machine learning-algoritmen samen met de Hallo verschillende gekoppeld afstemmen parameters (bekend als parameter vegen) die zijn die is afgestemd op het beantwoorden van vraag Hallo van belang Hello huidige gegevens.
* **'Aanbevolen' Hallo-oplossing bepalen** tooanswer Hallo vraag door het vergelijken van Hallo geslaagd metriek tussen alternatieve methoden.

> [!NOTE]
> **Voorkomen dat lekken**: lekken van gegevens kan worden veroorzaakt door Hallo opnemen van gegevens uit externe Hallo training gegevensset waarmee een model of de machine learning-algoritme toomake onrealistisch goede voorspellingen. Lekken is een veelvoorkomende reden waarom gegevenswetenschappers zenuwstelsel krijgen als ze voorspellende resultaten die te mooi toobe lijken true. Deze afhankelijkheden kunnen vaste toodetect zijn. tooavoid lekken vereist vaak tussen bouwen van een gegevensset analyse, maken van een model en evalueren Hallo nauwkeurigheid doorlopen. 
> 
> 

We bieden een [geautomatiseerde modelleren en rapportage hulpprogramma](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling) met TDSP die kunnen toorun via meerdere algoritmen en parameter duplicaten tooproduce een basislijn-model. Het resultaat ook een rapport met overzicht van de prestaties van elke combinatie model en parameter, met inbegrip van de variabele belang modelleren basislijn. Dit proces is ook herhaald als het verdere functie-engineering kunt station. 

### <a name="artifacts"></a>Artefacten
Hallo artefacten die in deze fase wordt geproduceerd zijn onder andere:

* [**Functie Sets**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): Hallo-functies die zijn ontwikkeld voor Hallo modellering worden beschreven in Hallo **functiesets** sectie Hallo **gegevensdefinitie** rapport. Het bevat verwijzingen toohello code toogenerate Hallo functies en beschrijving op hoe Hallo-functie is gegenereerd.
* [**Rapport model**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md): voor elk model dat wordt geprobeerd een standaard op basis van sjabloon rapport worden details weergegeven over elke experiment wordt geproduceerd.
* **Controlepunt besluit**: evalueren of Hallo model goed genoeg toodeploy is bezig met het productiesysteem tooa. Er zijn een aantal belangrijke vragen tooask:
  * Hallo model antwoord Hallo vraag met voldoende vertrouwen Hallo testgegevens gegeven? 
  * Een alternatieve benaderingen moet proberen: meer gegevens verzamelen, doen meer functie-engineering of experimenteren met andere algoritmen?


## <a name="4-deployment"></a>4. Implementatie

### <a name="goal"></a>Doel
* Modellen met een pipeline gegevens zijn geïmplementeerde tooa productie of productie-achtige omgeving voor de acceptatie van de eindgebruiker. 

### <a name="how-toodo-it"></a>Hoe toodo deze
de belangrijkste taak Hallo behandeld in deze fase:

* **Operationeel model Hallo**: Hallo model en pijplijn tooa productie of productie-achtige omgeving voor het verbruik van de toepassing implementeert.

#### <a name="41-operationalize-a-model"></a>4.1 mogelijk een model maken
Zodra u een set van modellen die ook uitvoeren hebt, kunnen u ze geoperationaliseerd voor andere toepassingen tooconsume. Afhankelijk van de bedrijfsvereisten hello, voorspellingen bestaan in realtime of op basis van de batch. toobe geoperationaliseerd, Hallo modellen hebben toobe weergegeven met een open API-interface die eenvoudig vanuit verschillende toepassingen zoals online websites, werkbladen, dashboards of line-of-business- en back-end-toepassingen wordt gebruikt. Zie voor voorbeelden van model uitoefening met een Azure Machine Learning-webservice [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md). Het is ook een best practice toobuild Telemetrie en bewaking in Hallo productiemodel en gegevens pijplijn geïmplementeerd toohelp hello met latere systeemstatus rapportage en het oplossen van problemen.  

### <a name="artifacts"></a>Artefacten
* Dashboard status van system health en sleutel metrische gegevens.
* Laatste modellering rapport met details van de implementatie.
* Definitieve oplossing architectuur document.

## <a name="5-customer-acceptance"></a>5. Aanvaarding van de klant

### <a name="goal"></a>Doel
* **Voltooien van de producten project Hallo**: Controleer of de Hallo pipeline, Hallo model en hun implementatie in een productieomgeving voldoet aan de doelstellingen van de klant zijn.

### <a name="how-toodo-it"></a>Hoe toodo deze
Er zijn twee belangrijke taken in deze fase verholpen:

* **Validatie van het systeem**: bevestigen Hallo geïmplementeerd model en pijplijn voldoet aan de behoeften van de klant.
* **Project aflevering**: toohello entiteit die toorun Hallo systeem in productie.

Hallo-klant moet valideert dat Hallo systeem voldoet aan de behoeften van hun bedrijf en het Hallo-antwoorden Hallo vragen met voldoende nauwkeurigheid toodeploy Hallo system tooproduction voor gebruik door de clienttoepassing. Alle Hallo documentatie is voltooid en gecontroleerd. Een aflevering van Hallo project toohello entiteit die verantwoordelijk is voor bewerkingen is voltooid. Deze entiteit kan bijvoorbeeld worden een IT- of klant gegevens wetenschappelijke team of een agent van Hallo klant die verantwoordelijk is voor het uitvoeren van Hallo systeem in productie. 

### <a name="artifacts"></a>Artefacten
Hallo belangrijkste artefacten die in deze laatste fase wordt geproduceerd is Hallo **afsluiten rapport van Project voor de klant**. Dit is technische Hallo-rapport met alle details van Hallo-project die handig toolearn over en Hallo systeem werkt. Een [afsluiten rapport](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md) sjabloon wordt geleverd door TDSP die kan worden gebruikt of aangepast voor specifieke client nodig heeft. 

## <a name="summary"></a>Samenvatting
Hallo [Team gegevens wetenschap proces lifecycle](http://aka.ms/datascienceprocess) is gemodelleerd naar een reeks stappen herhaald met informatie over taken Hallo toouse voorspellende modellen behoefte. Deze modellen kunnen worden geïmplementeerd in een productie-omgeving gebruikt toobe toobuild intelligente toepassingen. Hallo-doel van de levenscyclus van dit proces is toocontinue toomove een wetenschappelijke gegevensproject doorsturen naar het eindpunt van een duidelijke engagement. Het is weliswaar dat gegevenswetenschap oefening maakt in het onderzoek en -detectie wordt kunnen tooclearly communiceren deze taken tooyour team en uw klanten met een goed gedefinieerde set van artefacten die werknemers gestandaardiseerde sjablonen kunnen helpen voorkomen misverstand en verhoogt de kans op Hallo van een complexe gegevens wetenschap-project met succes is voltooid.

## <a name="next-steps"></a>Volgende stappen
Volledige end-to-end-scenario's die laten zien alle Hallo stappen in Hallo-proces voor **specifieke scenario's** worden ook gegeven. Ze worden weergegeven en gekoppeld aan de miniatuur beschrijvingen in Hallo [Team gegevens wetenschap proces scenario's](data-science-process-walkthroughs.md) onderwerp.

