---
title: aaaClean en voorbereiden van gegevens voor Azure Machine Learning | Microsoft Docs
description: Gegevens vooraf verwerken en schone tooprepare voor machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Taken tooprepare gegevens voor verbeterde machine learning
Vooraf verwerken en het opruimen van gegevens zijn belangrijke taken die normaal gesproken plaatsvinden moeten voordat gegevensset effectief kan worden gebruikt voor machine learning. Onbewerkte gegevens is vaak veel ruis veroorzaken en onbetrouwbare mogelijk ontbreken waarden. Met deze gegevens voor modellering kan misleidende resultaten opleveren. Deze taken deel uitmaken van Hallo Team gegevens wetenschap proces (TDSP) en doorgaans als volgt een initiële exploratie van een gegevensset gebruikt toodiscover en plan Hallo vooraf verwerken vereist. Voor meer instructies voor het Hallo TDSP proces gedetailleerde, Zie Hallo stappen in Hallo [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Vooraf verwerken en opschonen van taken, kan zoals Hallo data exploratie taak worden uitgevoerd in een groot aantal verschillende omgevingen, zoals SQL of Hive of Azure Machine Learning Studio, en met verschillende hulpprogramma's en talen, zoals het R- of Python, afhankelijk van waar uw gegevens zich opgeslagen en hoe deze is geformatteerd. Omdat TDSP iteratieve aard, deze taken kunnen worden uitgevoerd op verschillende stappen in de werkstroom Hallo van Hallo-proces.

Dit artikel bevat verschillende gegevensverwerking concepten en taken beschreven die kunnen worden uitgevoerd vóór of na het ophalen van gegevens in Azure Machine Learning.

Zie voor een voorbeeld van gegevensverkenning en vooraf verwerken die zijn uitgevoerd in Azure Machine Learning studio, Hallo [vooraf verwerken van gegevens in Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) video.

## <a name="why-pre-process-and-clean-data"></a>Waarom vooraf verwerken en de gegevens opschonen?
Concrete gegevens uit diverse bronnen worden verzameld en processen en onregelmatigheden of beschadigde gegevens inbreuk op Hallo kwaliteit van de gegevensset Hallo mag bevatten. Hallo typische data quality problemen die ontstaan zijn:

* **Onvolledig**: gegevens beschikt niet over kenmerken of met ontbrekende waarden.
* **Veel ruis veroorzaken**: gegevens foutieve records bevat of uitschieters.
* **Inconsistente**: gegevens bevat conflicterende records of afwijkingen.

Kwaliteitsgegevens is een vereiste voor kwaliteit voorspellende modellen. tooavoid 'garbagecollection in garbagecollection out' en de kwaliteit van de gegevens te verbeteren en daarom model prestaties, is het imperatieve tooconduct een toospot gegevens health scherm gegevens vroegtijdig problemen en bepaal Hallo overeenkomt gegevensverwerking en reiniging stappen.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>Wat zijn enkele typische gegevens health schermen die worden gebruikt?
We kunt Hallo algemene kwaliteit van de gegevens controleren door te controleren:

* aantal Hallo **records**.
* aantal Hallo **kenmerken** (of **functies**).
* Hallo-kenmerk **gegevenstypen** (nominaal, rangtelwoord of continu).
* aantal Hallo **ontbrekende waarden**.
* **-Opmaak** Hallo-gegevens.
  * Als gegevens Hallo in TSV- of CSV, controleert u dat Hallo kolom scheidingstekens en regel scheidingstekens altijd goed kolommen en lijnen scheiden.
  * Als Hallo gegevens in de HTML-indeling of XML-indeling, controleert u of Hallo gegevens is opgemaakt op basis van hun respectieve standaarden.
  * Bij het parseren van ook mogelijk nodig volgorde tooextract gestructureerde gegevens uit de semi-gestructureerde of ongestructureerde gegevens.
* **Inconsistente gegevensrecords**. Controleer het Hallo-bereik van waarden zijn toegestaan. bijvoorbeeld als Hallo gegevens studenten GPA, Controleer bevatten of Hallo GPA in Hallo aangewezen bereik is 0 spreken ~ 4.

Als u problemen met de gegevens gevonden **verwerken stappen** nodig die vaak omvat het opruimen van de ontbrekende waarden, gegevensnormalisatie, onderscheidende, tekst verwerking tooremove zijn en/of ingesloten tekens die mogelijk gevolgen hebben voor vervangen gegevensuitlijning, gemengde gegevenstypen gemeenschappelijk velden en anderen.

**Azure Machine Learning verbruikt juist opgemaakte tabelgegevens**.  Als het Hallo-gegevens is al in tabelvorm, kan gegevens vooraf verwerken rechtstreeks met Azure Machine Learning in Machine Learning Studio Hallo worden uitgevoerd.  Als gegevens niet in tabelvorm, als die het in XML-parsering is mogelijk vereist zijn in tooconvert Hallo gegevens tootabular formulier.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>Wat zijn enkele van de belangrijke taken Hallo in gegevens vooraf verwerken?
* **Gegevens gereinigd**: invullen of ontbrekende waarden detecteren en veel ruis veroorzaken en uitschieters verwijderen.
* **Gegevenstransformatie**: gegevens tooreduce dimensies en ruis normaliseren.
* **Gegevens vermindering**: Sample gegevensrecords of kenmerken voor gemakkelijker de verwerking van gegevens.
* **Gegevens onderscheidende**: converteren doorlopende kenmerken toocategorical kenmerken voor eenvoudig te gebruiken met bepaalde machine learning-methoden.
* **Tekst reinigen**: Verwijder de ingesloten tekens waardoor de uitlijning van gegevens voor bijvoorbeeld ingesloten tabbladen in een gegevensbestand met door tabs gescheiden ingesloten voor nieuwe regels die mogelijk worden verbroken records, enzovoort.

Hallo in de volgende secties bevatten informatie over enkele van de volgende stappen verwerken van gegevens.

## <a name="how-toodeal-with-missing-values"></a>Hoe toodeal met ontbrekende waarden?
toodeal met ontbrekende waarden, het is raadzaam toofirst identificeren Hallo reden voor toobetter ingang Hallo probleem Hallo ontbreken waarden. Typische ontbrekende waarde verwerking methoden zijn:

* **Verwijdering**: verwijderen van records met ontbrekende waarden
* **Vervanging testupdate worden uitgevoerd**: ontbrekende waarden vervangt door een dummy-waarde: bijvoorbeeld, *onbekende* voor categorische of 0 voor numerieke waarden.
* **Gemiddelde vervanging**: als de ontbrekende gegevens Hallo numerieke, Hallo ontbrekende waarden vervangt Hallo gemiddelde.
* **Regelmatige vervanging**: als de ontbrekende gegevens Hallo categorische, Hallo ontbrekende waarden vervangt de meest voorkomende item Hallo
* **Regressie vervanging**: gebruik een regressie methode tooreplace ontbrekende met waarden opgelost waarden.  

## <a name="how-toonormalize-data"></a>Hoe toonormalize gegevens?
Gegevens normalisatie opnieuw schaalt numerieke waarden tooa opgegeven bereik. Populaire gegevens normalisatie methoden zijn:

* **Min-Max normalisatie**: Lineair Hallo tooa gegevensbereik transformeren, spreken tussen 0 en 1, waarbij Hallo min-waarde is geschaald too0 en too1 max-waarde.
* **Z-score normalisatie**: gegevens op basis van gemiddelde en standaarddeviatie schalen: Hallo verschil tussen het Hallo-gegevens en gemiddelde Hallo delen door Hallo standaarddeviatie.
* **Decimale schalen**: Hallo gegevens schalen door bewegende Hallo decimaalteken van Hallo-kenmerkwaarde.  

## <a name="how-toodiscretize-data"></a>Hoe toodiscretize gegevens?
Gegevens kunnen worden onderscheiden door het converteren van doorlopende waarden toonominal kenmerken of intervallen. Er zijn een aantal manieren om dit te doen:

* **Gelijke breedte Binning**: Hallo bereik van alle mogelijke waarden van een kenmerk verdelen in groepen N Hallo dezelfde grootte en Hallo die waarden in een opslaglocatie toewijzen met Hallo bin nummer.
* **Met Binning gelijk hoogte**: verdelen Hallo bereik van alle waarden van een kenmerk in N groepen, elk met hetzelfde aantal exemplaren Hallo vervolgens Hallo waarden toewijzen die vallen in een opslaglocatie Hello bin nummer.  

## <a name="how-tooreduce-data"></a>Hoe tooreduce gegevens?
Er zijn verschillende methoden tooreduce gegevensgrootte voor gemakkelijker de afhandeling van gegevens. Afhankelijk van de gegevens grootte en Hallo domein kan Hallo volgende methoden worden toegepast:

* **Vastleggen van steekproeven**: Sample Hallo gegevensrecords en alleen Kies Hallo representatieve subset uit Hallo gegevens.
* **Kenmerk steekproeven**: alleen een subset van de belangrijkste kenmerken Hallo van Hallo gegevens selecteren.  
* **Aggregatie**: Hallo gegevens verdelen in groepen en Hallo getallen voor elke groep worden opgeslagen. Bijvoorbeeld: hello dagelijkse omzet cijfers van een keten restaurant via Hallo afgelopen 20 jaar kunnen worden geaggregeerd toomonthly omzet tooreduce Hallo grootte van Hallo-gegevens.  

## <a name="how-tooclean-text-data"></a>Hoe tooclean tekstgegevens?
**Tekstvelden in tabelgegevens** kunnen tekens die van invloed op grenzen die kolommen uitlijning en/of record bevatten. Voor bijvoorbeeld tabbladen in een bestand met door tabs gescheiden oorzaak kolom uitlijning van gegevenstypen ingesloten en ingesloten opsplitsen nieuwe-regeltekens record regels. Onjuiste tekstcodering verwerking tijdens het schrijven/lezen tekst leidt tooinformation verloren zijn gegaan, onbedoeld introductie van onleesbaar tekens, bijvoorbeeld nulwaarden en mogelijk ook invloed tekst te parseren. Zorgvuldige geparseerd en bewerkt mogelijk vereist zijn in de volgorde tooclean tekstvelden beschikbaar voor de juiste uitlijning en/of tooextract gestructureerde gegevens van niet-gestructureerde of semi-gestructureerde gegevens.

**Gegevensverkenning** biedt een weergave met een vroege in Hallo-gegevens. Een aantal problemen kan ongedekte tijdens deze stap en bijbehorende methoden kan worden toegepast tooaddress die problemen.  Het is belangrijk tooask vragen zoals wat Hallo bron van het Hallo-probleem is en hoe Hallo probleem kan zijn geïntroduceerd. Hierdoor kunnen ook bepalen op Hallo gegevensverwerking stappen die nodig toobe genomen tooresolve ze. Hallo soort insights een plan is tooderive van Hallo gegevens kan ook worden gebruikt tooprioritize Hallo gegevensverwerking inspanning.

## <a name="references"></a>Verwijzingen
> *Gegevensanalyse: Concepten en technieken*, Third Edition Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber en Jian Pei
> 
> 

