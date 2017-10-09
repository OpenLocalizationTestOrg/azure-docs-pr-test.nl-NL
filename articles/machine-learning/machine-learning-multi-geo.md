---
title: aaaMulti Geo Help-documentatie | Microsoft Docs
description: Meer informatie over hoe een werkruimte toocreate en publiceren van een webservice in een Azure-regio verschilt Hallo Zuid-centraal VS (SCUS) Azure-regio.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Help-documentatie voor meerdere geografische gebieden
Dit artikel wordt beschreven hoe u een werkruimte maken en publiceren van een webservice in verschillende Azure-regio's.  Hallo [Azure producten op de pagina regio](https://azure.microsoft.com/en-us/regions/services/) bevat gebieden waarin Azure Machine Learning beschikbaar is.

## <a name="create-a-workspace"></a>Een werkruimte maken
1. Meld u aan toohello klassieke Azure-Portal.
2. Klik op **+ nieuw** > **GEGEVENSSERVICES** > **MACHINE LEARNING** > **met snelle invoer**.  Onder **locatie** selecteren, zoals een andere regio **Zuidoost-Azië**.
   ![Multi-Geo-Help afbeelding 1][1]
3. Hallo-werkruimte selecteren en klik vervolgens op **aanmelden tooML Studio**.
   ![Multi-Geo-Help afbeelding 2][2]
4. U hebt nu een werkruimte in een andere regio die u net als elke andere werkruimte mag gebruiken. tooswitch tussen uw werkruimten uiterlijk toohello rechterbovenhoek van het scherm. Klik op Hallo dropdown, selecteer Hallo regio en selecteer vervolgens Hallo-werkruimte. Alles is lokale toohello werkruimte regio.  Alle webservices gemaakt op basis van een werkruimte wordt bijvoorbeeld Hallo zich in dezelfde regio Hallo werkruimte liggen.
   ![Multi-Geo-Help afbeelding 3][3]

## <a name="open-an-experiment-from-gallery"></a>Een experiment openen vanuit galerie
Als u een experiment vanuit galerie openen, kunt u ook selecteren welke regio gewenste toocopy Hallo experiment.

![Multi-Geo-Help afbeelding 4][4a]

## <a name="web-service-management"></a>Webservice beheren
tooprogrammatically voor het beheren van web-services, zoals voor de retraining, gebruik Hallo regiospecifieke adres:

* https://asiasoutheast.Management.azureml.NET
* https://europewest.Management.azureml.NET

### <a name="things-toonote"></a>Dingen toonote
1. U kunt alleen experimenten tussen werkruimten die deel uitmaken van toohello kopiëren dezelfde regio op deze manier. Als u toocopy experiment moet tussen de werkruimten in verschillende regio's, kunt u Hallo [PowerShell](http://aka.ms/amlps) commandlet [ *kopie AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish die. Een andere oplossing toopublish Hallo experiment in de galerie is in de modus voor niet-vermelde en opent u het in de werkruimte Hallo van Hallo andere regio.
2. Hallo regio selector wordt alleen weergegeven voor werkruimten voor één regio tegelijk.  
3. Een gratis werkruimte of gast (anonieme verificatie) werkruimte wordt gemaakt en gehost in Zuid-centraal VS  
4. Web-services op basis van een werkruimte in Zuidoost-Azië geïmplementeerd zal ook worden gehost in Zuidoost-Azië.  

## <a name="more-information"></a>Meer informatie
Stel een vraag op Hallo [Azure Machine Learning-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
