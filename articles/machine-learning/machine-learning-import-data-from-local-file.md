---
title: aaaImport gegevens uit een bestand in Azure Machine Learning Studio | Microsoft Docs
description: Meer informatie over hoe een trainingsgegevens tooupload bestand van de vaste schijf tooAzure Machine Learning Studio. Hiermee maakt u een module gegevensset in Hallo-werkruimte.
keywords: gegevens, gegevensindeling, gegevenstypen, gegevensbronnen, trainingsgegevens importeren
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Trainingsgegevens importeren uit een bestand op de harde schijf naar Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Meer informatie over hoe tooupload een gegevens-bestand van de vaste schijf toouse als trainingsgegevens in Azure Machine Learning Studio. Hallo gegevens door bestand te importeren, hebt u een gegevensset module klaar voor gebruik in uw werkruimte.

## <a name="steps-tooimport-data-from-a-local-file"></a>Stappen tooimport gegevens van een lokaal bestand
tooimport gegevens uit een lokale vaste schijf Hallo te volgen:

1. Klik op **+ nieuw** onderaan Hallo Hallo Machine Learning Studio-venster.
2. Selecteer **GEGEVENSSET** en **vanuit het lokale bestand**.
3. In Hallo **uploaden van een nieuwe gegevensset** dialoogvenster Bladeren toohello bestand dat u wilt dat tooupload
4. Voer een naam, gegevenstype Hallo identificeren en optioneel een beschrijving invoeren. Een beschrijving wordt aanbevolen - Hiermee kunt u toorecord alle kenmerken van dat het gewenste tooremember bij gebruik van Hallo gegevens in de toekomst Hallo Hallo-gegevens.
5. selectievakje Hallo **dit is de nieuwe versie Hallo van een bestaande gegevensset** kunt u tooupdate een bestaande gegevensset met nieuwe gegevens. Schakel dit selectievakje in en geef vervolgens Hallo-naam van een bestaande gegevensset.

![Uploaden van een nieuwe gegevensset](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Tijdens het uploaden ziet u een bericht dat uw bestand wordt geüpload. Uploaden tijd is afhankelijk van Hallo grootte van de snelheid van uw gegevens en Hallo van uw verbinding toohello-service. Als u Hallo bestand duurt lang duren weet, kunt u andere dingen in Machine Learning Studio doen terwijl u wacht. Hallo browser te sluiten wordt Hallo gegevens uploaden toofail veroorzaakt.

## <a name="dataset-module-is-ready-for-use"></a>DataSet-module is gereed voor gebruik
Nadat uw gegevens worden geüpload, wordt opgeslagen in een module gegevensset en is beschikbaar tooany experiment in uw werkruimte.

Wanneer u een experiment bewerkt, kunt u vinden Hallo gegevenssets die u hebt gemaakt in Hallo **mijn gegevenssets** lijst onder Hallo **gegevenssets opgeslagen** lijst in het modulepalet Hallo. U kunt slepen en neerzetten Hallo gegevensset op Hallo experimentcanvas als u wilt dat toouse Hallo gegevensset voor verdere analyse en machine learning.
