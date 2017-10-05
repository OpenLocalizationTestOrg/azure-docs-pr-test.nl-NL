---
title: Algemene bewerkingen in Machine Learning aanbevelingen API | Microsoft Docs
description: Azure ML aanbeveling voorbeeldtoepassing
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 0220bc17-3315-47d7-84a3-ef490263a343
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8d8efa93e820f4a745ed93c0f4d13b2438dfa1eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Inleiding met voorbeeldtoepassing van Recommendations-API
> [!NOTE]
> U moet beginnen met de aanbevelingen cognitieve API-Service in plaats van deze versie. De aanbevelingen cognitieve Service vervangt deze service en de nieuwe functies er zal worden ontwikkeld. Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.
> Meer informatie over [migreren naar de nieuwe cognitieve Service](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Doel
Dit document wordt het gebruik van de API van Azure Machine Learning aanbevelingen via een [voorbeeldtoepassing](https://code.msdn.microsoft.com/Recommendations-144df403).

Deze toepassing is niet bedoeld voor volledige functionaliteit bevatten, noch gebruikt de API's. Laat een aantal algemene bewerkingen om uit te voeren wanneer u eerst wilt afspelen met de Machine Learning aanbeveling-service. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-to-machine-learning-recommendation-service"></a>Inleiding tot Machine Learning aanbeveling service
Aanbevelingen via de Machine Learning aanbeveling service zijn ingeschakeld bij het samenstellen van een aanbeveling-model op basis van de volgende gegevens:

* Een opslagplaats voor de items die u wilt het beste, ook wel bekend als een catalogus
* Gegevens over het gebruik van items per gebruiker of sessie (dit kan worden verkregen na verloop van tijd via overname van gegevens, niet als onderdeel van de voorbeeld-app)

Nadat een aanbeveling model is gebouwd, kunt u deze gebruiken om te voorspellen objecten die een gebruiker mogelijk geïnteresseerd zijn in, volgens een reeks items (of één item) de gebruiker wordt geselecteerd.

Om het voorgaande scenario, het volgende in de service van Machine Learning aanbeveling te doen:

* Een model maken: dit is een logische container met de gegevens (catalogus en gebruik) en de voorspelling-modellen. Elke container model wordt geïdentificeerd via een unieke ID, dat wordt toegewezen wanneer deze wordt gemaakt. Deze ID heet de model-ID en het wordt gebruikt door de meeste van de API's. 
* Uploaden naar de catalogus: wanneer een model-container is gemaakt, kunt u koppelen aan een catalogus.

**Opmerking**: maken van een model en uploaden naar een catalogus worden doorgaans één keer uitgevoerd voor de levensduur van het model.

* Uploaden van gebruiksgegevens: gebruiksgegevens wordt toegevoegd aan de container model.
* Een aanbeveling model bouwen: nadat u voldoende gegevens hebt, kunt u de aanbeveling-model. Deze bewerking wordt de bovenste Machine Learning-algoritmen om een aanbeveling-model te maken. Elk build is gekoppeld aan een unieke ID. U moet een record van deze ID wordt behouden omdat het is nodig voor de functionaliteit van sommige API's.
* Bewaak het proces gebouw: een aanbeveling model build is een asynchrone bewerking het kan enkele minuten tot enkele uren duren, afhankelijk van de hoeveelheid gegevens (catalogus en gebruik) en de build-parameters. Daarom moet u de build bewaken. Een model aanbeveling wordt alleen gemaakt als de bijbehorende build voltooid is.
* (Optioneel) Kies een actieve aanbeveling model build: deze stap is alleen nodig als u meer dan één aanbeveling model ingebouwd in uw model-container hebt. Een aanvraag voor het ophalen van aanbevelingen zonder vermelding van het model actief aanbeveling wordt automatisch door het systeem naar de actieve standaard-build omgeleid. 

**Opmerking**: een model active aanbeveling productie gereed is en ze is opgebouwd voor productie werkbelasting. Dit wijkt af van een niet-actieve aanbeveling-model in een test-achtige-omgeving blijft (ook wel fasering genoemd).

* Aanbevelingen krijgen: nadat u een aanbeveling model hebt, kunt u de aanbevelingen voor één item of een lijst met items die u selecteert activeren. 

Aanbeveling ophalen wordt meestal worden aangeroepen voor een bepaalde periode. U kunt tijdens die periode, gebruiksgegevens omleiden naar het Machine Learning aanbeveling systeem waarmee deze gegevens worden toegevoegd aan de container opgegeven model. Wanneer u onvoldoende gebruiksgegevens hebt, kunt u een nieuw model voor de aanbeveling waarin de gebruiksgegevens voor aanvullende informatie over het kunt maken. 

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2013 of hoger
* Toegang tot het internet 
* Abonnement op de aanbevelingen API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning app Voorbeeldoplossing
Deze oplossing bevat de broncode, Voorbeeldgebruik, catalogusbestand en richtlijnen voor het downloaden van de pakketten die vereist voor de compilatie zijn.

## <a name="the-apis-used"></a>De API's gebruikt
De toepassing gebruikt Machine Learning aanbeveling functionaliteit via een subset van de beschikbare API's. De volgende API's worden getoond in de toepassing:

* Model maken: een logische container voor het opslaan van gegevens en aanbeveling modellen maken. Een model wordt aangeduid met een naam en u kunt meer dan één model met dezelfde naam maken.
* Catalogusbestand uploaden: gebruiken voor het uploaden van gegevens in de catalogus.
* Gebruik-bestand uploaden: gebruiken voor het uploaden van gebruiksgegevens.
* Activeren van build: gebruiken om een aanbeveling-model te maken.
* Bewaken van build-uitvoering: gebruiken voor het bewaken van de status van een aanbeveling model build.
* Kies een ingebouwde model voor aanbeveling: gebruiken om aan te geven welk model aanbeveling om standaard te gebruiken voor een bepaalde container in het model. Deze stap is nodig als u meer dan één aanbeveling model hebt en u wilt activeren van een niet-actieve build als het model actief aanbeveling.
* Ophalen van de aanbeveling: gebruik voor het ophalen van de aanbevolen items volgens een bepaald één item of een verzameling items. 

Zie de documentatie van Microsoft Azure Marketplace voor een volledige beschrijving van de API's. 

**Opmerking**: een model kan hebben verschillende builds gedurende een bepaalde periode (niet tegelijkertijd). Elk build wordt gemaakt met dezelfde of een bijgewerkte catalogus aanvullende gegevens en gebruiksgegevens.

## <a name="common-pitfalls"></a>Veelvoorkomende valkuilen
* U moet uw gebruikersnaam en uw primaire Microsoft Azure Marketplace-accountcode om uit te voeren van de voorbeeld-app opgeven.
* De voorbeeld-app opeenvolgend uitgevoerd mislukken. De stroom van de toepassing bevat maken, uploaden, maken van de monitor en aanbevelingen ophalen uit een vooraf gedefinieerde model; Daarom zal mislukken op opeenvolgende uitvoeren als u de naam van het model tussen aanroepen niet wijzigen.
* Aanbevelingen mogelijk zonder gegevens retourneren. De voorbeeld-app maakt gebruik van een zeer kleine catalogus en gebruik het bestand. Daarom heeft enkele items uit de catalogus geen aanbevolen items.

## <a name="disclaimer"></a>Vrijwaring
De voorbeeld-app is niet bedoeld om te worden uitgevoerd in een productieomgeving. De gegevens in de catalogus is erg klein en biedt geen een zinvolle aanbeveling-model. De gegevens is opgegeven als een demonstratie. 

