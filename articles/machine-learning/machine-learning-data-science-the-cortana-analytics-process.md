---
title: aaaWhat is Team gegevens wetenschap proces?  | Microsoft Docs
description: Hallo Team gegevens wetenschap proces is een systematische methode voor het bouwen van intelligente toepassingen die gebruikmaken van de geavanceerde analyses.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>Wat is Hallo Team gegevens wetenschap proces (TDSP)?
Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md) biedt een systematische aanpak toobuilding intelligente toepassingen waarmee teams van gegevens verzameld toocollaborate effectief kunt gedurende de volledige levenscyclus Hallo van activiteiten die nodig zijn tooturn deze toepassingen in producten. Hallo TDSP geeft een overzicht van een reeks stappen waarmee **richtlijnen** op toodefine Hallo probleem, instellen van Hallo-hulpprogramma's en omgeving die nodig zijn, hoe relevante gegevens analyseren, bouwen en evalueren van voorspellende modellen en implementeer deze modellen in zakelijke toepassingen. 

Hier volgen de stappen Hallo in **Team gegevens wetenschap proces**:  

![CAP-werkstroom](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

Hallo-proces is **iteratieve**: inzicht in de nieuwe en bestaande Hallo of verfijningen in Hallo model ontwikkeld en vereist dat eerder is voltooid in Hallo reeks stappen hoeven aanpassen. Bestaande organisatie-ontwikkeling en projectplanning processen zijn **eenvoudig aangepast** toowork Hello TDSP gedefinieerde volgorde van stappen. 

Hallo stappen Hallo bezig zijn in kaart gebracht en gekoppeld in Hallo [TDSP leertraject](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) en hieronder beschreven.  

## <a name="preparation-steps"></a>Voorbereidende stappen
## <a name="p1-plan-hello-analytics-project"></a>P1. Hallo analytics project plannen
Maak een project analytics door uw bedrijfsdoelen en problemen te definiëren. Ze worden opgegeven in termen van **bedrijfsvereisten**. Een centrale doel van deze stap is tooidentify Hallo belangrijke zakelijke variabelen (verkoop forecast of kans een volgorde dat frauduleuze, bijvoorbeeld Hallo) die Hallo analysis behoeften toopredict toosatisfy deze vereisten. Extra planning wordt vervolgens meestal essentiële toodevelop een goed begrip van Hallo **gegevensbronnen** nodig tooaddress Hallo doelstellingen van Hallo project vanuit een analytische perspectief. Het is niet ongewoon, bijvoorbeeld toofind die bestaande systemen toocollect nodig hebt en meld u aanvullende soorten gegevens tooaddress probleem Hallo en Hallo projectdoelstellingen te bereiken. Zie voor instructies [plannen van uw omgeving voor Hallo Team gegevens wetenschap proces](machine-learning-data-science-plan-your-environment.md) en [scenario's voor geavanceerde analyses in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Analyticsomgeving instellen
Een omgeving analytics voor het Hallo-Team gegevens wetenschap proces omvat verschillende onderdelen: 

* **gegevens werkruimten** waar Hallo gegevens tijdelijk worden opgeslagen voor analyse en modellering, 
* een **verwerkingsinfrastructuur** voor vooraf verwerken en modelleren Hallo gegevens verkennen
* een **runtime-infrastructuur** toooperationalize Hallo analytische modellen en Voer Hallo intelligent clienttoepassingen die Hallo modellen gebruiken.  

Hallo analytics infrastructuur die toobe setup moet is vaak deel van een omgeving die is gescheiden van de operationele systemen core. Maar deze doorgaans maakt gebruik van gegevens uit meerdere systemen binnen de onderneming Hallo als bronnen externe toohello bedrijf. Hallo analytics infrastructuur kan uitsluitend cloud-gebaseerde, of een lokale installatie of een hybride van Hallo twee. Zie voor opties [omgevingen van wetenschappelijke gegevens voor gebruik in Hallo Team gegevens wetenschap proces instellen](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Analytics-stappen:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Het opnemen van gegevens naar analytische Hallo-omgeving
de eerste stap Hallo is toobring Hallo relevante gegevens uit diverse bronnen, hetzij uit binnen of buiten Hallo enterprise, in een analytisch omgevingen waar Hallo gegevens kunnen worden verwerkt. Hallo **indeling** Hallo gegevens aan de bron kan afwijken van de vereiste door Hallo bestemming Hallo-indeling. Sommige gegevenstransformatie wellicht dus ook toobe Hallo opname tooling geraakte. Zie voor opties [gegevens laden in omgevingen met opslag voor analyses](machine-learning-data-science-ingest-data.md)

In aanvulling toohello initiële opname van gegevens zijn veel intelligente toepassingen vereist toorefresh Hallo gegevens regelmatig als onderdeel van een doorlopende leerproces. Dit kan worden gedaan door het instellen van een **data pipeline** of de werkstroom. Dit maakt deel uit van Hallo iteratieve deel van Hallo-proces met opnieuw te bouwen en opnieuw te evalueren Hallo analytische modellen die worden gebruikt door Hallo intelligent toepassing hello oplossing implementeren. Zie bijvoorbeeld [verplaatsen van gegevens uit een on-premises SQL server tooSQL Azure met Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Gegevens verkennen en voorverwerken
de volgende stap Hallo is tooobtain een beter begrip van Hallo gegevens door te kijken naar de **samenvattende statistieken** , relaties, en met behulp van dergelijke technieken **visualisatie**. Dit is ook waar problemen van **gegevenskwaliteit** en integriteit, zoals ontbrekende waarden, niet-overeenkomende typen gegevens en inconsistente gegevensrelaties worden verwerkt. Vooraf verwerken transformaties zijn gebruikte tooclean up Hallo onbewerkte gegevens voor verdere analyse en modellering kan plaatsvinden. Zie voor een beschrijving [tooprepare taakgegevens voor verbeterde machine learning](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Functies ontwikkelen
Gegevenswetenschappers in samenwerking met domein deskundigen, moeten omgaan Hallo vastleggen Hallo meest kenmerkende eigenschappen van gegevensset Hallo en dat mag meest gebruikte toopredict Hallo belangrijke zakelijke variabelen geïdentificeerd tijdens de planning. Deze nieuwe functies kunnen worden afgeleid van bestaande gegevens of moet u mogelijk aanvullende gegevens toobe verzameld. Dit proces wordt ook wel **functie-engineering** en is een Hallo de belangrijkste stappen bij het bouwen van een effectieve predictive analytics-systeem. Deze stap moet u een creative combinatie van domein-expertise en Hallo inzicht verkregen van Hallo gegevens verkenning stap. Zie voor instructies [functie-engineering in Hallo Team gegevens wetenschap proces](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Maak voorspellende modellen
Gegevenswetenschappers bouwen analytische modellen toopredict Hallo belangrijke variabelen geïdentificeerd door Hallo bedrijfsvereisten gedefinieerd in Hallo stap uit met gegevens die is opgeruimd en featurized plannen. Machine learning systemen ondersteunen meerdere **algoritmen modelleren** die een groot aantal gevallen van toepassing tooa zijn. Zie voor instructies [hoe toochoose algoritmen voor Team Azure Machine Learning](machine-learning-algorithm-choice.md).

Gegevenswetenschappers moeten de meest geschikte model Hallo voor hun taak voorspelling kiezen en gebeurt niet dat de resultaten van meerdere modellen gecombineerd toobe tooobtain Hallo beste resultaten moeten. Hallo is invoergegevens van modellering meestal verdeeld willekeurig drie delen:

* een set trainingsgegevens, 
* een validatie-gegevensset 
* een gegevensset testen 

Hallo-modellen zijn gebouwd met behulp van Hallo **set trainingsgegevens**. Hallo optimale combinatie van modellen (met parameters zijn afgestemd) is geselecteerd door Hallo modellen en meten Hallo voorspelling fouten voor Hallo **validatie gegevensset**. Ten slotte Hallo **testen gegevensset** gebruikte tooevaluate Hallo prestaties van Hallo gekozen model op onafhankelijke gegevens die niet gebruikte tootrain was is of valideren Hallo-model.  Zie voor procedures [hoe tooevaluate prestaties in Azure Machine Learning model](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Implementeren en gebruiken van modellen
Nadat we een set van modellen die ook uitvoeren hebben, worden ze **geoperationaliseerd** voor andere toepassingen tooconsume. Afhankelijk van de bedrijfsvereisten hello, voorspellingen bestaan in **realtime** of op een **batch** basis. toobe geoperationaliseerd, Hallo modellen hebben toobe weergegeven met een **open API interface** die eenvoudig verbruikt op verschillende toepassingen dergelijke online website, werkbladen, dashboards of line-of-business- en back-end-toepassingen. Zie [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Samenvatting en de volgende stappen
Hallo [Team gegevens wetenschap proces](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is gemodelleerd als een reeks stappen herhaald die **advies** op Hallo taken benodigde toouse advanced analytics toobuild een intelligente toepassingen. Elke stap biedt ook informatie over hoe toouse diverse Microsoft-technologieën toocomplete Hallo taken beschreven. 

Terwijl TDSP schrijft niet voor bepaalde soorten **documentatie** artefacten, het is een best practice toodocument Hallo-resultaten van Hallo gegevensverkenning, modellering en evaluatie en toosave Hallo relevante code zodat die analyse Hallo indien nodig kan worden herhaald. Hierdoor kunt ook hergebruik van Hallo analytics werkt wanneer u werkt aan andere toepassingen met betrekking tot dezelfde gegevens en taken van de voorspelling.

Volledige end-to-end-scenario's die laten zien alle Hallo stappen in Hallo-proces voor **specifieke scenario's** worden ook gegeven. Zie, bijvoorbeeld:

* [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md).
* [Met Spark op Azure HD.mdnsight Gegevenswetenschap](machine-learning-data-science-spark-overview.md)
* [Schaalbare Gegevenswetenschap in Azure Data Lake: een end-to-end-overzicht](machine-learning-data-science-process-data-lake-walkthrough.md)

