---
title: aaaExtend uw experiment met R | Microsoft Docs
description: Hoe Hallo tooextend Hallo-functionaliteit van Azure Machine Learning Studio Hallo R taal met behulp van de module R-Script uitvoeren.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a>Uw experiment uitbreiden met R
U kunt Hallo-functionaliteit van Azure Machine Learning Studio Hallo R taal uitbreiden met behulp van Hallo [R-Script uitvoeren] [ execute-r-script] module.

Deze module accepteert meerdere invoergegevenssets en resulteert in een enkel gegevensset als uitvoer. U kunt een R-script in Hallo typen **R-Script** parameter Hallo [R-Script uitvoeren] [ execute-r-script] module.

U openen elke invoerpoort van Hallo-module met behulp van code vergelijkbare toohello volgende:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Aanbieding geïnstalleerde pakketten
lijst met geïnstalleerde pakketten Hallo kunt wijzigen. Een lijst met geïnstalleerde pakketten vindt u in [R-pakketten wordt ondersteund door Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).

U kunt Hallo volledige, actuele lijst met geïnstalleerde pakketten ook opvragen door te voeren van de volgende code in Hallo Hallo [R-Script uitvoeren] [ execute-r-script] module:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Dit verzendt Hallo-lijst met pakketten toohello uitvoerpoort Hallo [R-Script uitvoeren] [ execute-r-script] module.
tooview Hallo pakket weergeven, zoals verbinding maken met een module conversie [converteren tooCSV] [ convert-to-csv] toohello links van de uitvoer van Hallo [R-Script uitvoeren] [ execute-r-script]-module, Voer Hallo experiment, klikt u vervolgens op Hallo-uitvoer van Hallo conversie module en selecteer **downloaden**. 

![Uitvoer van de module 'Converteren tooCSV' downloaden](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importeren van pakketten
U kunt pakketten die nog niet zijn geïnstalleerd met behulp van de volgende opdrachten in Hallo Hallo importeren [R-Script uitvoeren] [ execute-r-script] module:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

waar Hallo `my_favorite_package.zip` bestand bevat het pakket.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
