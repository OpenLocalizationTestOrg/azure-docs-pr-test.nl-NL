---
title: aaaLoad gegevens in Azure storage-omgevingen voor analyses | Microsoft Docs
description: Verplaatsen van gegevens tooand uit Azure Blob Storage
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a>Gegevens voor analysedoeleinden in opslagomgevingen laden
Hallo Team gegevens wetenschap proces vereist dat gegevens worden ingenomen of geladen in tal van andere opslag omgevingen toobe verwerkt of geanalyseerd op de meest geschikte manier Hallo in elke fase van het Hallo-proces. Gegevensbestemmingen meestal gebruikt voor verwerking bevatten Azure Blob Storage, Azure SQL-databases en SQL Server op virtuele machine in Azure HDInsight (Hadoop) en Azure Machine Learning. 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Dit **menu** tootopics waarin wordt beschreven hoe gegevens in een van deze tooingest omgevingen waar Hallo gegevens worden opgeslagen en verwerkt als doel is gekoppeld.

Technische en zakelijke behoeften, evenals de initiële locatie hello, opmaken en de grootte van uw gegevens Hallo doel omgevingen in welke Hallo gegevens toobe ingenomen tooachieve Hallo doelstellingen van de analyse moeten wordt bepaald. Het is niet ongewoon is voor een scenario toorequire gegevens toobe verplaatst tussen de verschillende omgevingen tooachieve Hallo diverse taken vereist tooconstruct een Voorspellend model. Deze reeks taken kan bijvoorbeeld bevatten gegevensverkenning, vooraf verwerken, opruimen, omlaag steekproeven en training model.

