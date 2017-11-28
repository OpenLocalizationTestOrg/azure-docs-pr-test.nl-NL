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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="7ad30-105">Trainingsgegevens importeren uit een bestand op de harde schijf naar Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="7ad30-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="7ad30-106">Meer informatie over hoe tooupload een gegevens-bestand van de vaste schijf toouse als trainingsgegevens in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="7ad30-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="7ad30-107">Hallo gegevens door bestand te importeren, hebt u een gegevensset module klaar voor gebruik in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="7ad30-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="7ad30-108">Stappen tooimport gegevens van een lokaal bestand</span><span class="sxs-lookup"><span data-stu-id="7ad30-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="7ad30-109">tooimport gegevens uit een lokale vaste schijf Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ad30-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="7ad30-110">Klik op **+ nieuw** onderaan Hallo Hallo Machine Learning Studio-venster.</span><span class="sxs-lookup"><span data-stu-id="7ad30-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="7ad30-111">Selecteer **GEGEVENSSET** en **vanuit het lokale bestand**.</span><span class="sxs-lookup"><span data-stu-id="7ad30-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="7ad30-112">In Hallo **uploaden van een nieuwe gegevensset** dialoogvenster Bladeren toohello bestand dat u wilt dat tooupload</span><span class="sxs-lookup"><span data-stu-id="7ad30-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="7ad30-113">Voer een naam, gegevenstype Hallo identificeren en optioneel een beschrijving invoeren.</span><span class="sxs-lookup"><span data-stu-id="7ad30-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="7ad30-114">Een beschrijving wordt aanbevolen - Hiermee kunt u toorecord alle kenmerken van dat het gewenste tooremember bij gebruik van Hallo gegevens in de toekomst Hallo Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="7ad30-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="7ad30-115">selectievakje Hallo **dit is de nieuwe versie Hallo van een bestaande gegevensset** kunt u tooupdate een bestaande gegevensset met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="7ad30-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="7ad30-116">Schakel dit selectievakje in en geef vervolgens Hallo-naam van een bestaande gegevensset.</span><span class="sxs-lookup"><span data-stu-id="7ad30-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![Uploaden van een nieuwe gegevensset](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="7ad30-118">Tijdens het uploaden ziet u een bericht dat uw bestand wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="7ad30-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="7ad30-119">Uploaden tijd is afhankelijk van Hallo grootte van de snelheid van uw gegevens en Hallo van uw verbinding toohello-service.</span><span class="sxs-lookup"><span data-stu-id="7ad30-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="7ad30-120">Als u Hallo bestand duurt lang duren weet, kunt u andere dingen in Machine Learning Studio doen terwijl u wacht.</span><span class="sxs-lookup"><span data-stu-id="7ad30-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="7ad30-121">Hallo browser te sluiten wordt Hallo gegevens uploaden toofail veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="7ad30-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="7ad30-122">DataSet-module is gereed voor gebruik</span><span class="sxs-lookup"><span data-stu-id="7ad30-122">Dataset module is ready for use</span></span>
<span data-ttu-id="7ad30-123">Nadat uw gegevens worden geüpload, wordt opgeslagen in een module gegevensset en is beschikbaar tooany experiment in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="7ad30-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="7ad30-124">Wanneer u een experiment bewerkt, kunt u vinden Hallo gegevenssets die u hebt gemaakt in Hallo **mijn gegevenssets** lijst onder Hallo **gegevenssets opgeslagen** lijst in het modulepalet Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ad30-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="7ad30-125">U kunt slepen en neerzetten Hallo gegevensset op Hallo experimentcanvas als u wilt dat toouse Hallo gegevensset voor verdere analyse en machine learning.</span><span class="sxs-lookup"><span data-stu-id="7ad30-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
