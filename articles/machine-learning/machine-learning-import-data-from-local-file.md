---
title: Gegevens importeren uit een bestand in Azure Machine Learning Studio | Microsoft Docs
description: Informatie over het uploaden van een gegevensbestand training van de harde schijf naar Azure Machine Learning Studio. Hiermee maakt u een gegevensset-module in de werkruimte.
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
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="fb25f-105">Trainingsgegevens importeren uit een bestand op de harde schijf naar Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="fb25f-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="fb25f-106">Informatie over het uploaden van een gegevensbestand van de vaste schijf om te gebruiken als trainingsgegevens in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fb25f-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="fb25f-107">Door het importeren van het gegevensbestand, hebt u een gegevensset module klaar voor gebruik in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="fb25f-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="fb25f-108">Stappen voor het importeren van gegevens uit een lokaal bestand</span><span class="sxs-lookup"><span data-stu-id="fb25f-108">Steps to import data from a local file</span></span>
<span data-ttu-id="fb25f-109">Om gegevens te importeren uit een lokale vaste schijf, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="fb25f-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="fb25f-110">Klik op **+ nieuw** aan de onderkant van het Machine Learning Studio-venster.</span><span class="sxs-lookup"><span data-stu-id="fb25f-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="fb25f-111">Selecteer **GEGEVENSSET** en **vanuit het lokale bestand**.</span><span class="sxs-lookup"><span data-stu-id="fb25f-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="fb25f-112">In de **uploaden van een nieuwe gegevensset** dialoogvenster, blader naar het bestand dat u wilt uploaden</span><span class="sxs-lookup"><span data-stu-id="fb25f-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="fb25f-113">Voer een naam, het gegevenstype te identificeren en optioneel een beschrijving invoeren.</span><span class="sxs-lookup"><span data-stu-id="fb25f-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="fb25f-114">Een beschrijving wordt aanbevolen - Hiermee kunt u voor het vastleggen van alle kenmerken van de gegevens die u dat wilt bij gebruik van de gegevens in de toekomst onthoudt.</span><span class="sxs-lookup"><span data-stu-id="fb25f-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="fb25f-115">Het selectievakje **dit is de nieuwe versie van een bestaande gegevensset** kunt u een bestaande gegevensset bijwerken met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="fb25f-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="fb25f-116">Klik op dit selectievakje in en geef vervolgens de naam van een bestaande gegevensset.</span><span class="sxs-lookup"><span data-stu-id="fb25f-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![Uploaden van een nieuwe gegevensset](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="fb25f-118">Tijdens het uploaden ziet u een bericht dat uw bestand wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="fb25f-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="fb25f-119">Uploaden tijd is afhankelijk van de grootte van uw gegevens en de snelheid van de verbinding met de service.</span><span class="sxs-lookup"><span data-stu-id="fb25f-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="fb25f-120">Als u dat het bestand wordt lange tijd duren, kunt u andere dingen in Machine Learning Studio doen terwijl u wacht.</span><span class="sxs-lookup"><span data-stu-id="fb25f-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="fb25f-121">Echter, de browser te sluiten zorgt ervoor dat het uploaden van gegevens is mislukt.</span><span class="sxs-lookup"><span data-stu-id="fb25f-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="fb25f-122">DataSet-module is gereed voor gebruik</span><span class="sxs-lookup"><span data-stu-id="fb25f-122">Dataset module is ready for use</span></span>
<span data-ttu-id="fb25f-123">Nadat uw gegevens worden geüpload, wordt opgeslagen in een module gegevensset en is beschikbaar voor alle experimenten in uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="fb25f-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="fb25f-124">Wanneer u een experiment bewerkt, vindt u de gegevenssets die u hebt gemaakt in de **mijn gegevenssets** lijst onder de **gegevenssets opgeslagen** lijst in het modulepalet.</span><span class="sxs-lookup"><span data-stu-id="fb25f-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="fb25f-125">U kunt slepen en neerzetten van de gegevensset naar het experimentcanvas wanneer u wilt de gegevensset gebruiken voor verdere analyse en machine learning.</span><span class="sxs-lookup"><span data-stu-id="fb25f-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
