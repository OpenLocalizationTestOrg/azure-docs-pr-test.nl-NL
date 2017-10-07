---
title: aaaExecute Python machine learning-scripts | Microsoft Docs
description: Overzichten ontwerp grondbeginselen ondersteuning voor Python-scripts in Azure Machine Learning en basic gebruiksscenario's, mogelijkheden en beperkingen.
keywords: Python machine learning pandas, python pandas, python-scripts, python-scripts uitvoeren
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Python-scripts voor Machine Learning uitvoeren in Azure Machine Learning Studio

Dit onderwerp beschrijft Hallo ontwerp grondbeginselen Hallo huidige ondersteuning voor Python-scripts in Azure Machine Learning. Hallo belangrijkste mogelijkheden worden ook beschreven, met inbegrip van:

- basic-gebruiksscenario's uitvoeren
- een experiment beoordelen in een webservice
- ondersteuning voor het importeren van de bestaande code
- Visualisaties exporteren
- onder supervisie Functieselectie uitvoeren
- enkele beperkingen begrijpen

[Python](https://www.python.org/) is een onmisbaar hulpmiddel bij Hallo hulpprogramma borst van veel gegevenswetenschappers. Heeft:

* een syntaxis elegante en beknopt 
* ondersteuning voor meerdere platforms 
* een enorme hoeveelheden krachtige bibliotheken en 
* volwassen ontwikkelingsprogramma's. 

Python wordt gebruikt in alle fasen van een werkstroom die doorgaans in machine learning-modellen worden gebruikt:

- gegevens opnemen en verwerken 
- functie constructie
- model trainen 
- validatie van
- implementatie van Hallo modellen

Azure Machine Learning Studio ondersteunt insluiten Python-scripts in diverse delen van een machine learning-experiment, en ze ook naadloos publiceren als een webservices op Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Principes van Python-scripts in Machine Learning

Hallo primaire interface tooPython in Azure Machine Learning Studio is via Hallo [Python Script uitvoeren] [ execute-python-script] module weergegeven in afbeelding 1.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Afbeelding 1. Hallo **Python Script uitvoeren** module.

Hallo [Python Script uitvoeren] [ execute-python-script] -module in de Azure ML Studio up toothree invoer accepteert en produceert up tootwo uitvoer (beschreven in de volgende sectie Hallo), zoals de analoog R hello [ R-Script uitvoeren] [ execute-r-script] module. Hello Python code toobe uitgevoerd, wordt in ingevoerd Hallo parameter box als een speciaal benoemde toegangspunt aangeroepen functie `azureml_main`. Hier vindt u belangrijke Hallo-ontwerp principes tooimplement gebruikt deze module:

1. *Moet idiomatische voor Python-gebruikers.* De meeste Python gebruikers rekening te houden met de code als functies in modules. Dus als een groot aantal uitvoerbare instructies in een module op het hoogste niveau is relatief zeldzame. Als gevolg hiervan neemt Hallo script vak ook een speciaal benoemde Python-functie als toojust tegenstelling tot een reeks instructies. Hallo objecten worden weergegeven in de functie Hallo zijn Python-bibliotheek Standaardtypen zoals [Pandas](http://pandas.pydata.org/) gegevensframes en [NumPy](http://www.numpy.org/) matrices.
2. *Hoogwaardige tussen lokale moet hebben en in de cloud uitvoeringen.* Hallo back-end gebruikt tooexecute Hallo Python-code op basis van [Anaconda](https://store.continuum.io/cshop/anaconda/), een veelgebruikte platformoverschrijdende wetenschappelijke Python-distributie. Het wordt geleverd met sluiten too200 van Hallo meest voorkomende Python-pakketten. Daarom gegevenswetenschappers voor foutopsporing en de code op hun lokale Azure Machine Learning-compatibele Anaconda-omgeving te kwalificeren. Gebruik vervolgens een bestaande ontwikkelomgeving, zoals [IPython](http://ipython.org/) notebook of [Python-Tools voor Visual Studio](http://aka.ms/ptvs), toorun als onderdeel van een Azure ML-experiment. Hallo `azureml_main` ingangspunt is een vanilla Python-functie en kan dus *** zonder Azure ML-specifieke code worden geschreven of Hallo SDK is geïnstalleerd.
3. *Moet naadloos samenstelbare met andere Azure Machine Learning-modules.* Hallo [Python Script uitvoeren] [ execute-python-script] module accepteert als invoer en uitvoer, standaard Azure Machine Learning-gegevenssets. de onderliggende structuur Hallo verbinding transparant en efficiënt hello Azure ML en Python runtimes. Dus kan Python worden gebruikt in combinatie met de bestaande Azure ML-werkstromen, inclusief verbindingen die gebruikmaken van R en SQLite. Een resultaat gegevens wetenschappelijk kan opstellen werkstromen die:
   * Python en Pandas gebruiken voor gegevens vooraf verwerken en opschonen
   * feed Hallo tooa SQL gegevenstransformatie, meerdere gegevenssets tooform functies toevoegen
   * Hallo-algoritmen gebruiken in Azure Machine Learning modellen trainen 
   * evalueren en verwerk Hallo resultaten weergeven in R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Basic-gebruiksscenario's in ML voor Python-scripts

In deze sectie we enkele Hallo basic maakt gebruik van Hallo enquête [Python Script uitvoeren] [ execute-python-script] module. Invoer toohello Python-module worden weergegeven als Pandas gegevensframes. Hallo functie moet retourneren één Pandas gegevensframe verpakt binnen een Python [reeks](https://docs.python.org/2/c-api/sequence.html) zoals een tuple, lijst of NumPy matrix. Hallo eerste element van deze reeks wordt vervolgens Hallo eerste uitvoerpoort van Hallo module geretourneerd. Dit schema wordt weergegeven in afbeelding 2.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Afbeelding 2. Toewijzing van poorten tooparameters invoer- en retourwaarde toooutput poort.

Meer gedetailleerde semantiek van hoe Hallo ingangspoorten toegewezen tooparameters Hallo downloaden `azureml_main` functie worden weergegeven in tabel 1:

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tabel 1. Toewijzing van ingangspoorten toofunction parameters.

Hallo-toewijzing tussen ingangspoorten en functieparameters is positionele:

- Hallo eerste verbonden invoerpoort is toegewezen toohello eerste parameter van Hallo-functie. 
- Hallo tweede invoer (indien verbonden) is toegewezen toohello tweede parameter van Hallo-functie.

Zie *Python voor gegevensanalyse* (O'Reilly 2012) door West McKinney voor meer informatie over Python Pandas en hoe deze gegevens gebruikte toomanipulate effectiever en efficiënter kan zijn. 


## <a name="translation-of-input-and-output-types"></a>De vertaling van invoer en uitvoer typen 
Invoergegevenssets in Azure ML zijn geconverteerde toodata frames in Pandas. Uitvoer gegevensframes omgezet back tooAzure ML gegevenssets. Hallo na conversies worden uitgevoerd:

1. Zo worden geconverteerd als tekenreeks en numerieke kolommen-is en de ontbrekende waarden in een gegevensset zijn geconverteerde too'NA' waarden in Pandas. Hallo dezelfde conversie wordt uitgevoerd op Hallo manier terug (NB-waarden in Pandas zijn geconverteerde toomissing waarden in de Azure ML).
2. Index aanvalsvectoren in Pandas worden niet ondersteund in Azure ML. Alle ingevoerde gegevensframes in Hallo Python functie hebben altijd een numerieke index van de 64-bits van 0 toohello aantal rijen min 1. 
3. Azure ML-gegevenssets geen dubbele kolomnamen en kolomnamen, die geen tekenreeksen zijn. Als een frame uitvoer-gegevens niet-numerieke kolommen bevat, Hallo framework aanroepen `str` op Hallo kolomnamen. Ook eventuele dubbele kolomnamen zijn automatisch vervormde tooinsure Hallo namen uniek zijn. Hallo-achtervoegsel (2) toegevoegd toohello eerste duplicaat, (3) de tweede dubbele toohello, enzovoort.


## <a name="operationalizing-python-scripts"></a>Operationele Python-scripts

Alle [Python Script uitvoeren] [ execute-python-script] modules die worden gebruikt in een score experiment worden aangeroepen wanneer gepubliceerd als een webservice. Afbeelding 3 ziet u bijvoorbeeld een score experiment met Hallo code tooevaluate één Python-expressie. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Afbeelding 3. Web-service voor het evalueren van een Python-expressie.

Een webservice die is gemaakt op basis van dit experiment:

- neemt als invoer een Python-expressie (als tekenreeks)
- verzendt het Python-interpreter toohello 
- retourneert een tabel die zowel Hallo expressie als resultaat Hallo geëvalueerd.


## <a name="importing-existing-python-script-modules"></a>Bestaande Python scriptmodules importeren

Een algemene gebruiksvoorbeeld voor veel gegevenswetenschappers is tooincorporate bestaande Python-scripts in Azure ML-experimenten. In plaats van het vereist dat alle code worden samengevoegd en in een vak één script worden geplakt, Hallo [Python Script uitvoeren] [ execute-python-script] module een zipbestand met Python-modules op de derde invoerpoort Hallo accepteert. Hallo-bestand is uitgepakt door Hallo uitvoering framework tijdens runtime en Hallo inhoud toohello bibliotheekpad van Python-interpreter Hallo worden toegevoegd. Hallo `azureml_main` toegangspunt dat deze modules kunt vervolgens rechtstreeks importeren door de functie.

Hallo-bestand met een eenvoudige "Hallo, wereld" functie Hello.py kunt u een voorbeeld.

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

Afbeelding 4. Gebruiker gedefinieerde functie in Hello.py-bestand.

Vervolgens maken we een bestand Hello.zip Hello.py met:

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

Afbeelding 5. ZIP-bestand met de gebruiker gedefinieerde Python-code.

Hallo zip-bestand uploaden als een gegevensset in Azure Machine Learning Studio. Vervolgens maken en uitvoeren van een experiment die gebruikmaakt van Hallo Python-code in Hallo Hello.zip bestand door het koppelen van toohello derde invoerpoort Hallo **Python Script uitvoeren** module, zoals weergegeven in deze afbeelding.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

Afbeelding 6. Voorbeeldexperiment door gebruiker gedefinieerde Python code geüpload als een zip-bestand.

Hallo module uitvoer laat zien dat Hallo zip-bestand is uitgepakt en die functie Hallo `print_hello` is uitgevoerd.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Afbeelding 7. Gebruiker gedefinieerde functie gebruikt in Hallo [Python Script uitvoeren] [ execute-python-script] module.


## <a name="working-with-visualizations"></a>Werken met visualisaties

Waarnemingspunten gemaakt met behulp van MatplotLib die kan worden weergegeven in de browser Hallo kunnen worden geretourneerd door Hallo [Python Script uitvoeren][execute-python-script]. Maar Hallo waarnemingspunten zijn niet automatisch omgeleid tooimages omdat ze bij gebruik van R. Dus Hallo gebruikers moet expliciet een waarnemingspunten tooPNG bestanden opslaan als ze zijn geretourneerd toobe back tooAzure Machine Learning. 

toogenerate installatiekopieën van MatplotLib, moet u Hallo procedure te volgen:

* Hallo back-end switch te "Door" van Hallo renderer Qt gebaseerde standaard 
* Maak een nieuw object van de afbeelding 
* Hallo as ophalen en het genereren van alle waarnemingspunten erin 
* Hallo afbeelding tooa PNG-bestand opslaan 

Dit proces wordt weergegeven in afbeelding 8 die u maakt een spreidingsgrafiek tekent matrix met Hallo scatter_matrix functie in Pandas na Hallo.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Afbeelding 8. Code toosave die matplotlib tooimages cijfers.

Afbeelding 9 toont een experiment die eerder weergegeven tooreturn worden uitgezet via Tweede uitvoerpoort Hallo Hallo-script gebruikt.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Afbeelding 9. Visualiseren waarnemingspunten gegenereerd op basis van Python-code.

Mogelijke tooreturn meerdere cijfers wordt door deze in verschillende afbeeldingen, hello Azure Machine Learning runtime opgehaald alle installatiekopieën en ze voor visualisatie kan toevoegen.


## <a name="advanced-examples"></a>Geavanceerde voorbeelden

Hallo Anaconda omgeving is geïnstalleerd in Azure Machine Learning bevat algemene pakketten zoals NumPy SciPy en Scikits meer. Deze pakketten kunnen effectief worden gebruikt voor verschillende gegevensverwerkingstaken in een machine learning-pijplijn. Als u bijvoorbeeld illustreren hello volgende experiment en script Hallo gebruik van ensemble overbrengen in Scikits meer toocompute functie belang scores voor een gegevensset. Hallo scores mag gebruikte tooperform onder supervisie Functieselectie voordat een andere ML-model wordt ingevoerd.

Ga als volgt Hallo Python gebruikt de functie toocompute Hallo belang scores en functies op basis van Hallo scores Hallo:

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

Afbeelding 10. Functies van de functie toorank door scores.
 Hallo volgende experiment vervolgens wordt berekend en retourneert Hallo belang scores van functies in Hallo 'Pima Indische Diabetes' gegevensset in Azure Machine Learning:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Afbeelding 11. Experiment toorank functies in Hallo Pima Indische Diabetes gegevensset.

## <a name="limitations"></a>Beperkingen
Hallo [Python Script uitvoeren] [ execute-python-script] heeft momenteel Hallo volgende beperkingen:

1. *De uitvoering van de sandbox.* Hallo Python-runtime is momenteel sandbox en, als gevolg hiervan kan geen toegang tot toohello netwerk of toohello lokaal bestandssysteem op een persistente manier. Alle bestanden lokaal opgeslagen zijn geïsoleerd en wordt verwijderd zodra het Hallo-module is voltooid. Hallo Python-code heeft geen toegang tot de meeste mappen op Hallo-machine die op wordt uitgevoerd, Hallo uitzondering wordt Hallo huidige map en de bijbehorende submappen.
2. *Een gebrek aan geavanceerde ontwikkeling en foutopsporing van ondersteuning.* Hallo Python-module biedt op dit moment geen ondersteuning van IDE-functies zoals intellisense en foutopsporing. Als Hallo-module is mislukt tijdens runtime, is hello volledige Python stack-trace ook beschikbaar. Maar deze moet worden weergegeven in het logboek voor de module Hallo Hallo. Momenteel wordt aangeraden dat u ontwikkelen en fouten opsporen in Python-scripts in een omgeving zoals IPython en vervolgens Hallo code in Hallo-module importeren.
3. *Enkele gegevens frame uitvoer.* Hallo Python-ingangspunt is alleen toegestaan tooreturn een één-frame als uitvoer. Het is niet mogelijk tooreturn die willekeurige Python-objecten, zoals getraind modellen back rechtstreeks toohello Azure Machine Learning-runtime. Zoals [R-Script uitvoeren][execute-r-script], die Hallo heeft dezelfde beperking, is het mogelijk in veel gevallen toopickle objecten in een byte matrix en ga daarna terug die binnen een gegevensframe.
4. *Onvermogen toocustomize Python installatie*. Hallo alleen manier tooadd aangepaste Python-modules is momenteel via Hallo zip-bestand mechanisme die eerder zijn beschreven. Dit is geschikt voor kleine modules, is het lastig voor grote modules (met name die met native DLLs) of een groot aantal modules. 

## <a name="conclusions"></a>Conclusie trekt
Hallo [Python Script uitvoeren] [ execute-python-script] module biedt een wetenschappelijk gegevens tooincorporate bestaande Python-code in de cloud gehoste machine learning werkstromen in Azure Machine Learning en tooseamlessly operationeel maken als onderdeel van een webservice. Hallo Python scriptmodule werkt natuurlijk samen met andere modules in Azure Machine Learning. Hallo-module kan worden gebruikt voor een bereik van taken van exploratie toopre verwerking van gegevens en het ophalen van de functies en vervolgens tooevaluation en naverwerking van Hallo resultaten. Hallo back-end runtime gebruikt voor de uitvoering is gebaseerd op Anaconda, een uitgebreid geteste en gebruikte Python-distributie. Deze back-end kunt u eenvoudig u tooon mededelingenbord bestaande code-elementen in de cloud Hallo.

We verwachten tooprovide aanvullende functionaliteit toohello [Python Script uitvoeren] [ execute-python-script] module, zoals Hallo mogelijkheid tootrain en modellen in Python operationeel en tooadd betere ondersteuning voor Hallo ontwikkeling en foutopsporing in Azure Machine Learning Studio.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [Python Developer Center](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
