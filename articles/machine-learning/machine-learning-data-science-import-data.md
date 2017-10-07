---
title: aaaImport gegevens naar Machine Learning Studio | Microsoft Docs
description: Hoe tooimport uw gegevens in Azure Machine Learning Studio van verschillende gegevensbronnen. Meer informatie over welke gegevenstypen en gegevensopmaak worden ondersteund.
keywords: gegevens, gegevensindeling, gegevenstypen, gegevensbronnen, trainingsgegevens importeren
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="dc4d8-105">Uw trainingsgegevens vanuit verschillende gegevensbronnen importeren in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="dc4d8-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="dc4d8-106">toouse uw eigen gegevens in Machine Learning Studio toodevelop en de trein een predictive analytics-oplossing, kunt u:</span><span class="sxs-lookup"><span data-stu-id="dc4d8-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="dc4d8-107">uploaden van gegevens uit een **lokaal bestand** voor tijd van de vaste schijf toocreate een gegevensset module in uw werkruimte</span><span class="sxs-lookup"><span data-stu-id="dc4d8-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="dc4d8-108">toegang tot gegevens uit een van de **online gegevensbronnen** terwijl uw experiment wordt uitgevoerd met behulp van Hallo [importgegevens] [ import-data] module</span><span class="sxs-lookup"><span data-stu-id="dc4d8-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="dc4d8-109">gegevens uit een andere Azure Machine learning **experimenteren** opgeslagen als een gegevensset</span><span class="sxs-lookup"><span data-stu-id="dc4d8-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="dc4d8-110">gegevens uit een on-premises **SQL Server-database**</span><span class="sxs-lookup"><span data-stu-id="dc4d8-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="dc4d8-111">Elk van deze opties wordt beschreven in een van de onderwerpen Hallo Hallo menu hieronder.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="dc4d8-112">Deze onderwerpen bevatten informatie over hoe tooimport van deze gegevens verschillende gegevensbronnen toouse in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="dc4d8-113">Er zijn een aantal voorbeeldgegevenssets beschikbaar in Machine Learning Studio die u voor trainingsgegevens gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="dc4d8-114">Zie voor meer informatie over deze [hello voorbeeldgegevenssets in Azure Machine Learning Studio gebruiken](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="dc4d8-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="dc4d8-115">Dit inleidende onderwerp wordt beschreven hoe tooget gegevens gereed voor gebruik in Machine Learning Studio ook en wordt beschreven welke gegevensindelingen en gegevenstypen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="dc4d8-116">Gegevens in Azure Machine Learning Studio klaar voor gebruik ophalen</span><span class="sxs-lookup"><span data-stu-id="dc4d8-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="dc4d8-117">Machine Learning Studio is ontworpen toowork met rechthoekige of tabellaire gegevens, zoals tekstgegevens die gescheiden of gestructureerde gegevens uit een database, maar in sommige gevallen niet-rechthoekige gegevens mogen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="dc4d8-118">Het is raadzaam als uw gegevens relatief schoon is.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="dc4d8-119">Dat wil zeggen, moet u tootake antwoord problemen zoals zonder aanhalingstekens tekenreeksen voordat u Hallo gegevens naar uw experiment uploaden.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="dc4d8-120">Er zijn echter modules in Machine Learning Studio waarmee manipuleren van gegevens binnen uw experiment beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="dc4d8-121">Afhankelijk van Hallo machine learning-algoritmen u wilt gebruiken, moet u mogelijk toodecide hoe u gegevens structurele problemen zoals ontbrekende waarden en sparse gegevens wordt verwerkt en er modules die u bij die helpen kunnen.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="dc4d8-122">Zoeken in Hallo **Data Transformation** sectie van het modulepalet Hallo voor modules die deze functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="dc4d8-123">U kunt op elk gewenst moment in uw experiment weergeven of downloaden Hallo-gegevens die wordt geproduceerd door een module door te klikken op de uitvoerpoort Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="dc4d8-124">Afhankelijk van de module hello, kunnen er verschillende Downloadinstellingen beschikbaar of hebt u mogelijk kunnen toovisualize Hallo gegevens in uw webbrowser in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="dc4d8-125">Opmaak en gegevenstypen worden ondersteund</span><span class="sxs-lookup"><span data-stu-id="dc4d8-125">Data formats and data types supported</span></span>
<span data-ttu-id="dc4d8-126">U kunt een aantal gegevenstypen in uw experiment importeren, afhankelijk van welke mechanisme u tooimport gegevens en waar deze vandaan gebruiken:</span><span class="sxs-lookup"><span data-stu-id="dc4d8-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="dc4d8-127">Tekstbestand (.txt)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-127">Plain text (.txt)</span></span>
* <span data-ttu-id="dc4d8-128">Door komma's gescheiden waarden (CSV met een koptekst (.csv) of zonder) (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="dc4d8-129">Door tabs gescheiden waarden (TSV met een koptekst (.tsv) of zonder) (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="dc4d8-130">Excel-bestand</span><span class="sxs-lookup"><span data-stu-id="dc4d8-130">Excel file</span></span>
* <span data-ttu-id="dc4d8-131">Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="dc4d8-131">Azure table</span></span>
* <span data-ttu-id="dc4d8-132">Hive-tabel</span><span class="sxs-lookup"><span data-stu-id="dc4d8-132">Hive table</span></span>
* <span data-ttu-id="dc4d8-133">SQL-databasetabel</span><span class="sxs-lookup"><span data-stu-id="dc4d8-133">SQL database table</span></span>
* <span data-ttu-id="dc4d8-134">OData-waarden</span><span class="sxs-lookup"><span data-stu-id="dc4d8-134">OData values</span></span>
* <span data-ttu-id="dc4d8-135">SVMLight gegevens (.svmlight) (Zie Hallo [SVMLight definitie](http://svmlight.joachims.org/) voor indeling informatie)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="dc4d8-136">Kenmerk Relation File Format (ARFF) gegevens (.arff) (Zie Hallo [ARFF definitie](http://weka.wikispaces.com/ARFF) voor indeling informatie)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="dc4d8-137">ZIP-bestand (.zip)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-137">Zip file (.zip)</span></span>
* <span data-ttu-id="dc4d8-138">R-object of de werkruimte-bestand (. RData)</span><span class="sxs-lookup"><span data-stu-id="dc4d8-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="dc4d8-139">Als u gegevens in een indeling zoals ARFF met metagegevens importeert, wordt in Machine Learning Studio deze metagegevens toodefine Hallo kop en het gegevenstype van elke kolom gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="dc4d8-140">Als u gegevens zoals TSV- of CSV-indeling waarin deze metagegevens niet importeert, gegevenstype Machine Learning Studio Hallo voor elke kolom van steekproeven Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="dc4d8-141">Als Hallo gegevens ook geen kolomkoppen, biedt Machine Learning Studio standaardnamen.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="dc4d8-142">U kunt expliciet opgeven of Hallo koppen en gegevenstypen voor kolommen met Hallo wijzigen [metagegevens bewerken][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="dc4d8-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="dc4d8-143">Hallo volgende **gegevenstypen** worden herkend door Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="dc4d8-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="dc4d8-144">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="dc4d8-144">String</span></span>
* <span data-ttu-id="dc4d8-145">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="dc4d8-145">Integer</span></span>
* <span data-ttu-id="dc4d8-146">dubbele</span><span class="sxs-lookup"><span data-stu-id="dc4d8-146">Double</span></span>
* <span data-ttu-id="dc4d8-147">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="dc4d8-147">Boolean</span></span>
* <span data-ttu-id="dc4d8-148">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="dc4d8-148">DateTime</span></span>
* <span data-ttu-id="dc4d8-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="dc4d8-149">TimeSpan</span></span>

<span data-ttu-id="dc4d8-150">Machine Learning Studio maakt gebruik van een interne gegevenstype aangeroepen ***gegevenstabel*** toopass gegevens tussen modules.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="dc4d8-151">U kunt uw gegevens expliciet converteren naar gegevens tabelindeling Hallo met [converteren tooDataset] [ convert-to-dataset] module.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="dc4d8-152">Elke module die indelingen dan gegevenstabel accepteert geconverteerd Hallo gegevens tooData tabel achtergrond voordat deze de volgende module toohello wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="dc4d8-153">U kunt indien nodig, gegevenstabel naar CSV, TSV, ARFF, of SVMLight notatie met andere modules conversie converteren.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="dc4d8-154">Zoeken in Hallo **gegevens indeling conversies** sectie van het modulepalet Hallo voor modules die deze functies worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc4d8-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
