---
title: aaaManage experimenteren iteraties in Machine Learning Studio | Microsoft Docs
description: Hoe toomanage experimenteren iteraties in Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Iteraties van experimenten beheren in Azure Machine Learning Studio
Een predictive Analytics-model te ontwikkelen is een iteratief proces - terwijl u Hallo wijzigt verschillende functies en parameters van uw experiment de resultaten geconvergeerd tot u tevreden bent dat u een getraind en doeltreffend model hebt. Sleutel toothis proces is bijhouden Hallo verschillende herhalingen van uw experiment parameters en configuraties.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

U kunt eerder uitgevoerde bekijken van uw experimenten op elk gewenst moment in volgorde toochallenge bezoekt, en uiteindelijk bevestigen of eerdere veronderstellingen verfijnen. Wanneer u een experiment uitvoert, Machine Learning Studio wordt bijgehouden Hallo uitvoeren, waaronder gegevensset, module en poort verbindingen en -parameters. Dit overzicht wordt ook vastgelegd runtime informatie zoals de begin- en stoptijden, logboekberichten en uitvoeringsstatus van resultaten. U kunt zoeken terug op een van deze wordt uitgevoerd op elk moment tooreview Hallo overzicht van uw experiment en tussenliggende resultaten. U kunt zelfs uw experiment toolaunch eerder werd uitgevoerd in een nieuwe fase van de query en detectie gebruiken op uw pad toocreating eenvoudige, complexe of zelfs ensemble oplossingen voor het modelleren.

> [!NOTE]
> Wanneer u een eerder uitgevoerde van een experiment bekijkt, wordt deze versie van Hallo experiment is vergrendeld en kan niet worden bewerkt. U kunt echter een kopie opslaan door te klikken op **SAVE AS** en het geven van een nieuwe naam voor het Hallo-exemplaar. Machine Learning Studio wordt geopend Hallo nieuwe kopie, die u kunt vervolgens bewerken en uitvoeren. Dit exemplaar van uw experiment is beschikbaar in Hallo **EXPERIMENTEN** lijst samen met uw experimenten.
> 
> 

## <a name="viewing-hello-prior-run"></a>Weergave Hallo voorafgaande uitvoeren
Wanneer u een experiment geopend die u hebt ten minste één keer uitgevoerd hebt, kunt u voorafgaand aan uitvoering van Hallo experiment door te klikken op Hallo weergeven **voorafgaande uitvoeren** in deelvenster Hallo-eigenschappen.

Stel bijvoorbeeld dat u een experiment maken en uitvoeren van versies van it op 11:23 11:42 en 11:55. Als u de laatste uitvoering Hallo van Hallo experiment (11:55) opent en klikt u op **voorafgaande uitvoeren**, Hallo-versie die u op 11:42 uitvoerde wordt geopend.

## <a name="viewing-hello-run-history"></a>Weergave Hallo geschiedenis uitvoeren
U kunt alle Hallo eerder uitgevoerde van een experiment weergeven door te klikken op **weergave uitvoeren geschiedenis** in een open experiment.

Stel bijvoorbeeld dat u een experiment maken met de Hallo [lineaire regressie] [ linear-regression] module en u wilt dat tooobserve Hallo effect van het wijzigen van Hallo-waarde van **leertempo** op de resultaten van uw experiment. U uitvoeren Hallo experiment meerdere keren met verschillende waarden voor deze parameter als volgt:

| De waarde voor Learning | Begintijd uitvoering |
| --- | --- |
| 0.1 |11-9-2014 4:18:58 pm |
| 0.2 |11-9-2014 4:24:33 pm |
| 0.4 |11-9-2014 4:28:36 uur |
| 0.5 |11-9-2014 4:33:31 pm |

Als u op **weergave uitvoeren geschiedenis**, ziet u een lijst van deze wordt uitgevoerd:

![Voorbeeld van de geschiedenis uitvoeren][runhistory]

Klik op een van deze wordt uitgevoerd tooview een momentopname van Hallo op Hallo toen u het experiment. Hallo configuratie, parameterwaarden, opmerkingen en resultaten zijn alle behouden toogive u een volledig overzicht van uw experiment die wordt uitgevoerd.

> [!TIP]
> toodocument uw iteraties van Hallo experiment, kunt u wijzigen Hallo titel telkens wanneer u deze uitvoert, kunt u Hallo bijwerken **samenvatting** Hallo experimenteren in het eigenschappendeelvenster hello, en u kunt toevoegen of bijwerken van opmerkingen over afzonderlijke modules toorecord uw wijzigingen. Hallo-titel, de samenvatting en de module opmerkingen worden opgeslagen met elke run van Hallo experiment.
> 
> 

Hallo-lijst met experimenten in Hallo **EXPERIMENTEN** tabblad in Machine Learning Studio altijd Hallo meest recente versie van een experiment weergegeven. Als u een eerder uitgevoerde van Hallo experiment openen (met behulp van **voorafgaande uitvoeren** of **weergave uitvoeren geschiedenis**), kunt u de conceptversie toohello terugkeren door te klikken op **weergave uitvoeren geschiedenis** en te selecteren Hallo herhaling met een **status** van **bewerkbaar**.

## <a name="iterating-on-a-previous-run"></a>Op een eerder uitgevoerde doorlopen
Wanneer u klikt op **voorafgaande uitvoeren** of **weergave uitvoeren geschiedenis** en opent een eerder werd uitgevoerd, kunt u een voltooide experiment weergeven in de modus alleen-lezen.

Als u een herhaling van uw experiment die beginnen met Hallo manier waarop u het hebt geconfigureerd voor een eerder uitgevoerde toobegin wilt, u kunt dit doen door openen Hallo uitvoeren en te klikken **SAVE AS**. Hiermee maakt u een nieuw experiment met een nieuwe naam, een lege uitvoeringsgeschiedenis alle Hallo-onderdelen en parameterwaarden Hallo vorige uitvoeren. Dit nieuwe experiment wordt vermeld in Hallo **EXPERIMENTEN** tabblad in Machine Learning Studio-startpagina hello, en u kunt wijzigen en uitvoeren, initiëren van een nieuwe uitvoeringsgeschiedenis voor deze herhaling van uw experiment. 

Stel dat u hebt Hallo experiment geschiedenis wordt weergegeven in de vorige sectie Hallo uitvoeren. U wilt dat tooobserve wat er gebeurt wanneer u Hallo instellen **leertempo** too0.4 parameter en probeer verschillende waarden voor Hallo **aantal training epoches** parameter.

1. Klik op **weergave uitvoeren geschiedenis** en open Hallo herhaling van Hallo experiment die u hebt uitgevoerd om 4:28:36 uur (u stelt waarin Hallo parameter waarde too0.4).
2. Klik op **SAVE AS**.
3. Voer een nieuwe titel en klikt u op Hallo **OK** vinkje. Een nieuw exemplaar van Hallo experiment wordt gemaakt.
4. Hallo wijzigen **aantal training epoches** parameter.
5. Klik op **uitvoeren**.

U kunt nu doorgaan toomodify en uitvoeren van deze versie van uw experiment het bouwen van een nieuwe uitvoeringsgeschiedenis toorecord uw werk.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
