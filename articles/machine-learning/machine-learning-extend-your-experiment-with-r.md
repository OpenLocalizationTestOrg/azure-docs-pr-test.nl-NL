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
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="a8220-103">Uw experiment uitbreiden met R</span><span class="sxs-lookup"><span data-stu-id="a8220-103">Extend your experiment with R</span></span>
<span data-ttu-id="a8220-104">U kunt Hallo-functionaliteit van Azure Machine Learning Studio Hallo R taal uitbreiden met behulp van Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="a8220-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="a8220-105">Deze module accepteert meerdere invoergegevenssets en resulteert in een enkel gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a8220-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="a8220-106">U kunt een R-script in Hallo typen **R-Script** parameter Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="a8220-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="a8220-107">U openen elke invoerpoort van Hallo-module met behulp van code vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a8220-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="a8220-108">Aanbieding geïnstalleerde pakketten</span><span class="sxs-lookup"><span data-stu-id="a8220-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="a8220-109">lijst met geïnstalleerde pakketten Hallo kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a8220-109">hello list of installed packages can change.</span></span> <span data-ttu-id="a8220-110">Een lijst met geïnstalleerde pakketten vindt u in [R-pakketten wordt ondersteund door Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8220-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="a8220-111">U kunt Hallo volledige, actuele lijst met geïnstalleerde pakketten ook opvragen door te voeren van de volgende code in Hallo Hallo [R-Script uitvoeren] [ execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="a8220-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="a8220-112">Dit verzendt Hallo-lijst met pakketten toohello uitvoerpoort Hallo [R-Script uitvoeren] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="a8220-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="a8220-113">tooview Hallo pakket weergeven, zoals verbinding maken met een module conversie [converteren tooCSV] [ convert-to-csv] toohello links van de uitvoer van Hallo [R-Script uitvoeren] [ execute-r-script]-module, Voer Hallo experiment, klikt u vervolgens op Hallo-uitvoer van Hallo conversie module en selecteer **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="a8220-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Uitvoer van de module 'Converteren tooCSV' downloaden](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="a8220-115">Importeren van pakketten</span><span class="sxs-lookup"><span data-stu-id="a8220-115">Importing packages</span></span>
<span data-ttu-id="a8220-116">U kunt pakketten die nog niet zijn geïnstalleerd met behulp van de volgende opdrachten in Hallo Hallo importeren [R-Script uitvoeren] [ execute-r-script] module:</span><span class="sxs-lookup"><span data-stu-id="a8220-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="a8220-117">waar Hallo `my_favorite_package.zip` bestand bevat het pakket.</span><span class="sxs-lookup"><span data-stu-id="a8220-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
