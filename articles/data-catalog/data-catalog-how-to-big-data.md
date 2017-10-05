---
title: Werken met gegevensbronnen 'big data' | Microsoft Docs
description: Hoe kan ik artikel patronen voor het gebruik van Azure Data Catalog met 'big data' gegevensbronnen, waaronder Azure Blob Storage, Azure Data Lake en Hadoop HDFS is gemarkeerd.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 001d80ce42f0e87276e59d70dffb75eb561d96cd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-work-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="98f15-103">Werken met big gegevensbronnen in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="98f15-103">How to work with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="98f15-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="98f15-104">Introduction</span></span>
<span data-ttu-id="98f15-105">**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert.</span><span class="sxs-lookup"><span data-stu-id="98f15-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="98f15-106">Het is alle over mensen helpen detecteren, begrijpen en gebruiken van gegevensbronnen en helpt organisaties meer waarde ophalen van hun bestaande gegevensbronnen, met inbegrip van big data.</span><span class="sxs-lookup"><span data-stu-id="98f15-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="98f15-107">**Azure Data Catalog** biedt ondersteuning voor de registratie van Azure Blog van Storage-blobs en mappen alsook Hadoop HDFS-bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="98f15-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="98f15-108">De semi-gestructureerde aard van deze gegevensbronnen biedt hoge mate van flexibiliteit.</span><span class="sxs-lookup"><span data-stu-id="98f15-108">The semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="98f15-109">Echter, naar de meest waarde niet ophalen uit het registreren van deze met **Azure Data Catalog**, gebruikers moeten rekening houden met de rangschikking van de gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="98f15-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="98f15-110">Mappen als logische gegevenssets</span><span class="sxs-lookup"><span data-stu-id="98f15-110">Directories as logical data sets</span></span>
<span data-ttu-id="98f15-111">Een algemene patroon voor het ordenen van grote gegevensbronnen is mappen behandelen als logische gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="98f15-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span></span> <span data-ttu-id="98f15-112">Op het hoogste niveau mappen worden gebruikt voor het definiëren van een gegevensset terwijl submappen Definieer partities en de bestanden die ze bevatten de gegevens zelf worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="98f15-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span></span>

<span data-ttu-id="98f15-113">Een voorbeeld van dit patroon is mogelijk:</span><span class="sxs-lookup"><span data-stu-id="98f15-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="98f15-114">In dit voorbeeld vertegenwoordigen vehicle_maintenance_events en location_tracking_events logische gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="98f15-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="98f15-115">Elk van deze mappen bevat gegevensbestanden die zijn ingedeeld op jaar en maand in submappen.</span><span class="sxs-lookup"><span data-stu-id="98f15-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="98f15-116">Elk van deze mappen zich mogelijk honderden of duizenden bestanden.</span><span class="sxs-lookup"><span data-stu-id="98f15-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="98f15-117">In dit patroon registratie van afzonderlijke bestanden met **Azure Data Catalog** waarschijnlijk niet logisch.</span><span class="sxs-lookup"><span data-stu-id="98f15-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="98f15-118">In plaats daarvan de mappen met daarin de gegevenssets die relevant zijn voor de gebruikers die werken met de gegevens worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="98f15-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="98f15-119">Verwijzing naar gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="98f15-119">Reference data files</span></span>
<span data-ttu-id="98f15-120">Er is een aanvullende patroon voor het opslaan van sets van verwijzingsgegevens als afzonderlijke bestanden.</span><span class="sxs-lookup"><span data-stu-id="98f15-120">A complementary pattern is to store reference data sets as individual files.</span></span> <span data-ttu-id="98f15-121">Deze gegevenssets kunnen worden beschouwd als de 'kleine'-zijde van big data en zijn vaak net als bij dimensies in een model analytische gegevens.</span><span class="sxs-lookup"><span data-stu-id="98f15-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span></span> <span data-ttu-id="98f15-122">Referentie-gegevensbestanden bevat records die worden gebruikt voor context voor het merendeel van de bestanden elders in de big data-archief opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="98f15-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span></span>

<span data-ttu-id="98f15-123">Een voorbeeld van dit patroon is mogelijk:</span><span class="sxs-lookup"><span data-stu-id="98f15-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="98f15-124">Wanneer een analist of gegevens wetenschappelijk samen met de gegevens in de grotere directory-structuren werkt, kan de gegevens in deze verwijzing bestanden worden gebruikt om meer gedetailleerde informatie voor entiteiten die alleen door de naam of ID worden aangeduid in de grotere gegevensset te geven.</span><span class="sxs-lookup"><span data-stu-id="98f15-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span></span>

<span data-ttu-id="98f15-125">In dit patroon is het verstandig om te registreren van de gegevensbestanden van de afzonderlijke verwijzing met **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="98f15-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="98f15-126">Elk bestand vertegenwoordigt een set gegevens en elkaar kan worden aangetekend en afzonderlijk gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="98f15-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="98f15-127">Alternatieve patronen</span><span class="sxs-lookup"><span data-stu-id="98f15-127">Alternate patterns</span></span>
<span data-ttu-id="98f15-128">De patronen die zijn beschreven in de vorige sectie zijn twee manieren die een big data store kan worden georganiseerd, maar elke implementatie verschilt.</span><span class="sxs-lookup"><span data-stu-id="98f15-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="98f15-129">Ongeacht hoe uw gegevensbronnen zijn gestructureerd, bij het registreren van gegevensbronnen met big **Azure Data Catalog**, ligt de nadruk op het registreren van de bestanden en mappen die vertegenwoordigen de gegevenssets van waarde naar anderen binnen uw de organisatie.</span><span class="sxs-lookup"><span data-stu-id="98f15-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span></span> <span data-ttu-id="98f15-130">Registratie van alle bestanden en mappen kan bruikbaar blijft de catalogus, waardoor het moeilijker voor gebruikers kunnen vinden die ze nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="98f15-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="98f15-131">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="98f15-131">Summary</span></span>
<span data-ttu-id="98f15-132">Registreren van gegevensbronnen met **Azure Data Catalog** zorgt ervoor dat ze eenvoudiger te detecteren en begrijpen.</span><span class="sxs-lookup"><span data-stu-id="98f15-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span></span> <span data-ttu-id="98f15-133">Door te registreren en aantekeningen maken van de big data-bestanden en mappen die logische gegevenssets vertegenwoordigen, kunt u gebruikers zoeken en gebruiken van de grote gegevensbronnen die ze nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="98f15-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span></span>
