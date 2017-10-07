---
title: aaaCommon bewerkingen in Machine Learning aanbevelingen API Hallo | Microsoft Docs
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
redirect_document_id: True
ms.openlocfilehash: da16767134a1386617e1184e4a4850f1f346e972
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="recommendations-api-sample-application-walkthrough"></a>Inleiding met voorbeeldtoepassing van Recommendations-API
> [!NOTE]
> U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie. Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld. Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.
> Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)
> 
> 

## <a name="purpose"></a>Doel
Dit document beschrijft Hallo gebruik van hello Azure Machine Learning aanbevelingen API via een [voorbeeldtoepassing](https://code.msdn.microsoft.com/Recommendations-144df403).

Deze toepassing is niet de volledige functionaliteit van beoogde tooinclude noch gebruiken alle Hallo API's. Laat een aantal algemene bewerkingen tooperform als u wilt dat eerst tooplay Hello Machine Learning aanbeveling-service. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="introduction-toomachine-learning-recommendation-service"></a>Inleiding tooMachine Learning aanbeveling-service
Aanbevelingen via Hallo Machine Learning aanbeveling service zijn ingeschakeld bij het samenstellen van een aanbeveling-model op basis van Hallo gegevens te volgen:

* Een opslagplaats voor de gewenste toorecommend, ook wel bekend als een catalogus Hallo-items
* Gegevens weergeven van het Hallo-gebruik van items per gebruiker of sessie (dit kan worden verkregen na verloop van tijd via overname van gegevens, niet als onderdeel van de voorbeeld-app Hallo)

Nadat een aanbeveling model is gebouwd, kunt u toopredict items die een gebruiker mogelijk geïnteresseerd zijn in, volgens tooa reeks items (of één item) Hallo gebruiker selecteert.

tooenable Hallo vorige scenario, komen in de volgende Hallo Hallo Machine Learning aanbeveling service:

* Een model maken: dit is een logische container met Hallo gegevens (catalogus en gebruik) en Hallo voorspelling modellen. Elke container model wordt geïdentificeerd via een unieke ID, dat wordt toegewezen wanneer deze wordt gemaakt. Deze ID heet Hallo model-ID en het wordt gebruikt door de meeste Hallo API's. 
* Uploaden van toocatalog: wanneer een model-container is gemaakt, kunt u een catalogus tooit koppelen.

**Opmerking**: maken van een model en uploadt tooa catalogus worden doorgaans één keer uitgevoerd voor Hallo model levenscyclus.

* Uploaden van gebruiksgegevens: Hiermee voegt u informatie over het gebruik gegevens toohello model container.
* Een aanbeveling model bouwen: nadat u voldoende gegevens hebt, kunt u Hallo aanbeveling model maken. Deze bewerking wordt Hallo bovenste Machine Learning-algoritmen toocreate een aanbeveling-model. Elk build is gekoppeld aan een unieke ID. U moet een record van deze ID tookeep omdat het is nodig voor Hallo-functionaliteit van sommige API's.
* Monitor Hallo maken: een aanbeveling model build is een asynchrone bewerking het kan enkele minuten tooseveral uur, afhankelijk van de hoeveelheid gegevens (catalogus en gebruik) Hallo duren en Hallo build-parameters. Daarom moet u toomonitor Hallo build. Een model aanbeveling wordt alleen gemaakt als de bijbehorende build voltooid is.
* (Optioneel) Kies een actieve aanbeveling model build: deze stap is alleen nodig als u meer dan één aanbeveling model ingebouwd in uw model-container hebt. Aanvraag tooget aanbevelingen zonder vermelding Hallo active aanbeveling model wordt automatisch door Hallo system toohello standaard active build omgeleid. 

**Opmerking**: een model active aanbeveling productie gereed is en ze is opgebouwd voor productie werkbelasting. Dit wijkt af van een niet-actieve aanbeveling-model in een test-achtige-omgeving blijft (ook wel fasering genoemd).

* Aanbevelingen krijgen: nadat u een aanbeveling model hebt, kunt u de aanbevelingen voor één item of een lijst met items die u selecteert activeren. 

Aanbeveling ophalen wordt meestal worden aangeroepen voor een bepaalde periode. U kunt tijdens die periode, gebruik gegevens toohello Machine Learning aanbeveling systeem, dat deze container gegevens toohello opgegeven model voegt omleiden. Wanneer u onvoldoende gebruiksgegevens hebt, kunt u een nieuw model voor de aanbeveling waarin Hallo aanvullende gebruiksgegevens maken. 

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2013 of hoger
* Toegang tot het internet 
* Abonnement toohello aanbevelingen API (https://datamarket.azure.com/dataset/amla/recommendations).

## <a name="azure-machine-learning-sample-app-solution"></a>Azure Machine Learning app Voorbeeldoplossing
Deze oplossing bevat de broncode hello, Voorbeeldgebruik catalogusbestand en richtlijnen toodownload hello-pakketten die vereist voor compileren zijn.

## <a name="hello-apis-used"></a>Hallo API's gebruikt
Hallo-toepassing gebruikt Machine Learning aanbeveling functionaliteit via een subset van de beschikbare API's. Hallo die volgende API's in de toepassing hello worden uitgelegd:

* Model maken: een logische container toohold gegevens en aanbeveling modellen maken. Een model wordt aangeduid met een naam en u kunt meer dan één model maken met de Hallo dezelfde naam.
* Catalogusbestand uploaden: tooupload catalogusgegevens gebruiken.
* Gebruik-bestand uploaden: tooupload gebruiksgegevens gebruiken.
* Activeren van build: toocreate een aanbeveling-model gebruiken.
* Bewaken van build-uitvoering: toomonitor Hallo status van een aanbeveling model build gebruiken.
* Kies een ingebouwde model voor aanbeveling: tooindicate welke aanbeveling model toouse wordt standaard gebruikt voor een bepaalde container in het model. Deze stap is nodig als u meer dan één aanbeveling model hebt en u wilt dat een niet-actieve als Hallo active aanbeveling model bouwen tooactivate.
* Ophalen van de aanbeveling: tooretrieve aanbevolen items op basis van tooa gegeven één item of een verzameling items gebruiken. 

Zie voor een volledige beschrijving van de API's Hallo Hallo-documentatie voor Microsoft Azure Marketplace. 

**Opmerking**: een model kan hebben verschillende builds gedurende een bepaalde periode (niet tegelijkertijd). Elk build is gemaakt met de Hallo dezelfde of een bijgewerkte catalogus aanvullende gegevens en gebruiksgegevens.

## <a name="common-pitfalls"></a>Veelvoorkomende valkuilen
* Tooprovide moet u uw gebruikersnaam en Microsoft Azure Marketplace primaire sleutel toorun Hallo sample app voor je account.
* Actieve Hallo voorbeeld-app mislukt opeenvolgend. Hallo toepassing stroom bevat maken, uploaden, Hallo monitor bouwen en aanbevelingen ophalen uit een vooraf gedefinieerde model; Daarom zal mislukken op opeenvolgende uitvoeren als u de modelnaam Hallo tussen aanroepen niet wijzigen.
* Aanbevelingen mogelijk zonder gegevens retourneren. Hallo voorbeeld-app maakt gebruik van een zeer kleine catalogus en gebruik het bestand. Daarom heeft enkele items uit de catalogus Hallo geen aanbevolen items.

## <a name="disclaimer"></a>Vrijwaring
Hallo voorbeeld-app is niet bedoeld toobe uitvoeren in een productieomgeving. Hallo-gegevens die zijn opgegeven in de catalogus Hallo is erg klein en biedt geen een zinvolle aanbeveling-model. Hallo-gegevens is opgegeven als een demonstratie. 

