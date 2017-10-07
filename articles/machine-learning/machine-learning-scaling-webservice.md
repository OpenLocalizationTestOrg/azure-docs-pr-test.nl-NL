---
title: aaaHow tooincrease gelijktijdigheid van een Azure Machine Learning-webservice | Microsoft Docs
description: Meer informatie over hoe tooincrease gelijktijdigheid van een Azure Machine Learning-webservice door extra eindpunten toe te voegen.
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: Azure machine learning-webservices, uitoefening, schaal, eindpunt, gelijktijdigheid van taken
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Een Azure Machine Learning-webservice schalen door extra eindpunten toe te voegen
> [!NOTE]
> Dit onderwerp wordt beschreven technieken toepasselijke tooa **klassieke** Machine Learning-webservice. 
> 
> 

Standaard elke gepubliceerde webservice geconfigureerde toosupport is 20 gelijktijdige aanvragen en mag maximaal 200 gelijktijdige aanvragen. Hoewel Hallo klassieke Azure-portal een manier tooset deze waarde biedt, Azure Machine Learning optimaliseert automatisch Hallo instelling tooprovide Hallo optimale prestaties van uw web-service en portal Hallo-waarde wordt genegeerd. 

Als u van plan toocall Hallo API met een hogere belasting bent dan een waarde van het maximumaantal gelijktijdige aanroepen van 200 wordt ondersteunen, moet u meerdere eindpunten maken op Hallo dezelfde webservice. U kunt uw load willekeurig distribueren voor alle hiervan.

Hallo schalen van een webservice is een algemene taak. Een aantal redenen tooscale zijn toosupport meer dan 200 gelijktijdige aanvragen, beschikbaarheid via meerdere eindpunten te verbeteren of afzonderlijke eindpunten voor Hallo webservice leveren. U kunt Hallo schaal verhogen door toe te voegen extra eindpunten voor Hallo dezelfde webservice via [klassieke Azure-portal](https://manage.windowsazure.com/) of Hallo [Azure Machine Learning-webservice](https://services.azureml.net/) portal.

Zie voor meer informatie over het toevoegen van nieuwe eindpunten [eindpunten maken](machine-learning-create-endpoint.md).

Houd er rekening mee dat met een aantal hoge gelijktijdigheid schadelijk als u geen Hallo API met een navenant hoge frequentie bellen. U ziet sporadisch time-outs en/of pieken in Hallo latentie als u een relatief lage belasting voor een API die is geconfigureerd voor hoge belasting.

Hallo die synchrone API's worden meestal gebruikt in situaties waarin een lage latentie gewenst is. Latentie hier impliceert Hallo tijd het duurt voordat een aanvraag van Hallo API toocomplete en niet-account voor elke vertragingen in het netwerk. Stel dat u hebt een API met een latentie van 50-ms. toofully gebruiken voor de beschikbare capaciteit Hallo met vertraging niveau Hoog- en maximumaantal gelijktijdige aanroepen = 20, moet u toocall na deze API 20 * 1000 / 50 = 400 keren per seconde. Dit verder uitbreiden, kunt een maximumaantal gelijktijdige aanroepen van 200 u toocall Hallo API 4000 keren per seconde, ervan uitgaande dat een 50 ms latentie.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
