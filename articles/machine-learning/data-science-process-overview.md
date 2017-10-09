---
title: overzicht van het Team gegevens wetenschap proces aaaAzure | Microsoft Docs
description: Biedt een gegevens wetenschappelijke methodologie toodeliver predictive analytics-oplossingen en intelligente toepassingen.
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
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Overzicht van het team gegevens wetenschap proces

Hallo Team gegevens wetenschap proces (TDSP) is een flexibele, herhalende gegevens wetenschappelijke methodologie toodeliver predictive analytics-oplossingen en intelligente toepassingen efficiënt. TDSP verbetert teamsamenwerking en leren. Het bevat een distillatie van Hallo best practices en structuren van Microsoft en anderen in Hallo bedrijfstak die Hallo geslaagde implementatie van gegevens wetenschappelijke initiatieven vergemakkelijken. Hallo-doel is altijd bewust Hallo voordelen van het programma analytics toohelp bedrijven.

Dit artikel bevat een overzicht van TDSP en de belangrijkste onderdelen. We bieden een algemene beschrijving van Hallo proces hier die kan worden geïmplementeerd met tal van hulpprogramma's. Een gedetailleerdere beschrijving van Hallo projecttaken en functies die zijn betrokken bij de levenscyclus van Hallo proces Hallo vindt u in extra gekoppelde onderwerpen. Hulp bij hoe tooimplement hello TDSP met behulp van een specifieke set Microsoft-programma's en infrastructuur gebruiken we tooimplement hello TDSP in onze teams is ook beschikbaar.

## <a name="key-components-of-hello-tdsp"></a>Belangrijke onderdelen van Hallo TDSP

TDSP omvat Hallo volgende hoofdonderdelen:

- Een **gegevens wetenschappelijke lifecycle** definitie
- Een **gestandaardiseerd projectstructuur**
- **Infrastructuur en resources** voor gegevens wetenschappelijke projecten
- **Hulpprogramma's** voor de projectuitvoering van


## <a name="data-science-lifecycle"></a>Levenscyclus van wetenschappelijke gegevens

Hallo Team gegevens wetenschap proces (TDSP) biedt een levenscyclus toostructure Hallo ontwikkeling van uw gegevens wetenschap-projecten. Hallo lifecycle bevat een overzicht van Hallo stappen van de start-toofinish die projecten meestal volgt wanneer ze worden uitgevoerd.

Als u een andere gegevens wetenschappelijke levensduur, zoals gebruikt [heldere DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) of uw organisatie zelf aangepast proces, kunt u TDSP op basis van een taak in de context van de ontwikkeling Hallo Hallo levenscycli. Op een hoog niveau hebben deze verschillende methoden veel gemeen. 

Deze levenscyclus beheren is ontworpen voor wetenschap-projecten voor gegevens die worden geleverd als onderdeel van intelligente toepassingen. Deze toepassingen implementeren machine learning of kunstmatige intelligence modellen voor predictive analytics. Experimentele gegevens wetenschap of ad-hoc analytics projecten kunnen ook profiteren van dit proces. Maar in dergelijke gevallen een aantal stappen Hallo mogelijk niet nodig.    

Hallo TDSP lifecycle bestaat uit vijf belangrijke fasen die iteratief worden uitgevoerd:

* **Wat voor bedrijven**
* **Gegevensverzameling en begrijpen**
* **Modeling**
* **Implementatie**
* **Acceptatie van de klant**

Hier volgt een visuele representatie van Hallo **Team gegevens wetenschap proces lifecycle**. 

![Levenscyclus van TDSP](./media/data-science-process-overview/tdsp-lifecycle.png) 

Hallo doelstellingen, taken en documentatie artefacten voor elke fase van de levenscyclus van Hallo in TDSP worden beschreven in Hallo [Team gegevens wetenschap proces lifecycle](data-science-process-lifecycle.md) onderwerp. Deze taken en de artefacten zijn gekoppeld aan Projectrollen:

- Oplossing architect
- Projectmanager
- Gegevenswetenschapper
- Projectleider 

Hallo biedt volgende diagram een rasterweergave Hallo-taken (in blauw) en artefacten (in groen) die zijn gekoppeld aan elke fase van de levenscyclus hello (op de horizontale as Hallo) voor deze rollen (op de verticale as Hallo). 

![TDSP-functies-en-taken](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>De structuur gestandaardiseerde project

Met alle projecten een mapstructuur delen en het gebruik van sjablonen voor de project-documenten, kunt u gemakkelijk voor Hallo team leden toofind informatie over hun projecten. Alle code en documenten worden opgeslagen in een versiebeheersysteem (VCS) zoals Git of TFS Subversion tooenable teamsamenwerking. Bijhouden van taken en functies in een flexibele project traceringssysteem zoals Jira Rally, Visual Studio Team Services Hiermee kan dichter bijhouden Hallo-code voor de afzonderlijke onderdelen. Dergelijke bijhouden kan ook teams tooobtain beter geschatte kosten. TDSP raadt aan om het maken van een afzonderlijke opslagplaats voor elk project op Hallo VCS voor versiebeheer, informatiebeveiliging en samenwerking. Hallo gestandaardiseerd structuur voor alle projecten helpt build institutionele kennis over Hallo-organisatie.

We bieden sjablonen voor Hallo mapstructuur en de vereiste documenten op standaardlocaties. Deze mapstructuur ordent Hallo-bestanden die code voor gegevensverkenning en uitpakken van de functie bevatten en die model iteraties opnemen. Deze sjablonen maken het gemakkelijker voor team leden toounderstand werk gedaan door anderen en tooadd nieuwe leden tooteams. Het is gemakkelijk tooview en update documentsjablonen in markdown-indeling. Gebruik sjablonen tooprovide controlelijsten met belangrijke vragen voor elk project tooinsure dat Hallo probleem goed gedefinieerde is en de producten die voldoen aan Hallo kwaliteit verwacht. Voorbeelden zijn:

- een project Freelance toodocument Hallo zakelijke probleem en de omvang van Hallo-project
- rapporten toodocument Hallo gegevensstructuur en statistieken van onbewerkte gegevens Hallo
- model rapporten toodocument Hallo afgeleide functies
- model maatstaven voor prestaties zoals ROC curven of muis


![TDSP-mappen](./media/data-science-process-overview/tdsp-dir-structure.png)

Hallo-mapstructuur kan worden gekloond van [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).

## <a name="infrastructure-and-resources-for-data-science-projects"></a>Infrastructuur en resources voor gegevens wetenschappelijke projecten

TDSP bevat aanbevelingen voor het beheren van gedeelde analytics en opslaginfrastructuur zoals:

- cloud-bestandssystemen voor het opslaan van gegevenssets 
- databases
- BIG data (Hadoop of Spark) clusters 
- machine learning-services. 

Hallo analytics en opslag infrastructuur kan zich op Hallo cloud of on-premises. Dit is waar de onbewerkte gegevens en verwerkte gegevenssets worden opgeslagen. Deze infrastructuur kunt reproduceerbare analyse. Ook voorkomt u dubbele, wat tooinconsistencies en onnodige infrastructuurkosten leiden kan. Hulpprogramma's zijn opgegeven tooprovision Hallo gedeelde bronnen, ze bijhouden en toestaan dat elk lid team tooconnect toothose resources veilig. Het is ook een goede gewoonte projectleden die u maakt een consistente compute-omgeving hebben. Andere teamleden kunnen repliceren en experimenten te valideren.

Hier volgt een voorbeeld van een team werkt aan meerdere projecten en delen van de verschillende onderdelen van de cloud analytics infrastructuur.

![TDSP-infrastructuur](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>Hulpprogramma's voor de projectuitvoering van

Inleiding tot processen in de meeste organisaties is lastig. Hulpprogramma's opgegeven tooimplement Hallo gegevens wetenschappelijke processen en lifecycle kunt lagere Hallo barrières tooand Hallo consistentie van de vaststelling verhogen. TDSP biedt een eerste set hulpprogramma's en scripts toojump start acceptatie van TDSP binnen een team. Het helpt tevens Hallo gangbare taken in Hallo gegevens wetenschappelijke lifecycle zoals gegevensverkenning en basislijn modellering automatiseren. Er is een goed gedefinieerde structuur opgegeven voor personen toocontribute hulpprogramma's in hun team gedeelde code opslagplaats gedeeld. Deze resources kunnen vervolgens worden gebruikt door andere projecten binnen Hallo team of organisatie Hallo. TDSP plan ook tooenable Hallo bijdragen van hulpprogramma's en hulpmiddelen toohello hele community. Hallo TDSP hulpprogramma's kunnen worden gekloond van [Github](https://github.com/Azure/Azure-TDSP-Utilities).


## <a name="next-steps"></a>Volgende stappen

[Team gegevens wetenschappelijke processen: De rollen en taken](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) geeft een overzicht van Hallo personeel belangrijke functies en de bijbehorende taken voor een wetenschappelijke-team voor gegevens die op dit proces standaardiseert. 
