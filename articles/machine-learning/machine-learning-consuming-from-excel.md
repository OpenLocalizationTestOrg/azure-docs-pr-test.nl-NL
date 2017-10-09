---
title: een Machine Learning-webservice vanuit Excel aaaConsume | Microsoft Docs
description: Een Azure Machine Learning-webservice vanuit Excel gebruiken
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Een Azure Machine Learning-webservice gebruiken vanuit Excel
 Azure Machine Learning Studio maakt het eenvoudig toocall webservices rechtstreeks vanuit Excel zonder Hallo moet toowrite code.

Als u Excel 2013 (of hoger) of Excel Online gebruikt, wordt aangeraden dat u Excel Hallo [Excel-invoegtoepassing](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Stappen
Een webservice publiceert. [Deze pagina](machine-learning-walkthrough-5-publish-web-service.md) wordt uitgelegd hoe toodo deze. Hallo Excel-werkmap functie is momenteel alleen ondersteund voor de aanvraag/antwoord-services die één uitvoer (dat wil zeggen, een enkel scoreprofiel label). 

Zodra u een webservice hebt, klik op Hallo **WEBSERVICES** sectie aan de linkerkant Hallo van Hallo studio, en selecteer vervolgens Hallo web service tooconsume in Excel.

**Klassieke webservice**

1. Op Hallo **DASHBOARD** tabblad voor Hallo-webservice een rij voor Hallo is **aanvragen/reacties** service. Als deze service één uitvoer heeft, ziet u Hallo **Excel-werkmap downloaden** koppeling in die rij.
   
    ![][1]
2. Klik op **Excel-werkmap downloaden**.

**Nieuwe webservice**

1. Selecteer in hello Azure Machine Learning-webservice portal **verbruiken**.
2. Hallo verbruiken in op pagina Hallo **Web-verbruik serviceopties** sectie, klikt u op Hallo Excel-pictogram.

**Hallo werkmap**

1. Open Hallo-werkmap.
2. Er verschijnt een beveiligingswaarschuwing; Klik op Hallo **bewerken inschakelen** knop.
   
    ![][2]
3. Een beveiligingswaarschuwing weergegeven. Klik op Hallo **inhoud inschakelen** knop toorun macro's in het werkblad.
   
    ![][3]
4. Zodra de macro's zijn ingeschakeld, wordt een tabel wordt gegenereerd. Kolommen in blauw zijn vereist als invoer in Hallo RRS-webservice of **PARAMETERS**. Houd er rekening mee Hallo uitvoer Hallo RRS-service, **VOORSPELDE waarden** in groen. Wanneer alle kolommen voor een bepaalde rij zijn ingevuld, Hallo werkmap automatisch Hallo score berekenen voor API-aanroepen en Hallo berekend resultaten worden weergegeven.
   
    ![][4]
5. tooscore meer dan een rij, voorspelde opvulling Hallo tweede rij met gegevens en Hallo waarden worden gegenereerd. U kunt zelfs meerdere rijen in één keer plakken.

U Hallo Excel-functies (grafieken, power-kaart, voorwaardelijke opmaak, enz.) kunt gebruiken met Hallo voorspelde waarden toohelp Hallo gegevens visualiseren.    

## <a name="sharing-your-workbook"></a>Delen van uw werkmap
Voor Hallo macro's toowork, moet uw API-sleutel deel uitmaken van Hallo werkblad. Dat betekent dat u alleen met entiteiten/personen die u vertrouwt Hallo werkmap moet delen.

## <a name="automatic-updates"></a>Automatische updates
In deze situaties wordt een RRS-aanroep uitgevoerd:

1. Hallo eerst een rij heeft de inhoud in alle bijbehorende **PARAMETERS**
2. Telkens wanneer u een van de Hallo **PARAMETERS** wijzigingen in een rij die alle waren bijbehorende **PARAMETERS** ingevoerd.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
