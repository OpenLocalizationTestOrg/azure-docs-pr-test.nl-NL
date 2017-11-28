---
title: aaaHow toowork met gegevensbronnen 'big data' | Microsoft Docs
description: Hoe tooarticle markeren patronen voor het gebruik van Azure Data Catalog met 'big data' gegevensbronnen, waaronder Azure Blob Storage, Azure Data Lake en Hadoop HDFS.
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
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="1abc8-103">Hoe toowork met big data in Azure Data Catalog gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="1abc8-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="1abc8-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="1abc8-104">Introduction</span></span>
<span data-ttu-id="1abc8-105">**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert.</span><span class="sxs-lookup"><span data-stu-id="1abc8-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="1abc8-106">Het is over medewerkers detecteren, begrijpen en gebruiken van gegevensbronnen helpen en helpt organisaties tooget meerwaarde van hun bestaande gegevensbronnen, met inbegrip van big data.</span><span class="sxs-lookup"><span data-stu-id="1abc8-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="1abc8-107">**Azure Data Catalog** ondersteunt Hallo registratie van Azure Blog van Storage-blobs en mappen alsook Hadoop HDFS-bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="1abc8-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="1abc8-108">Hallo semi-gestructureerde aard van deze gegevensbronnen biedt hoge mate van flexibiliteit.</span><span class="sxs-lookup"><span data-stu-id="1abc8-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="1abc8-109">Echter tooget optimaal zich kunnen registreren met Hallo **Azure Data Catalog**, gebruikers moeten rekening houden met het Hallo-gegevensbronnen worden ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="1abc8-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="1abc8-110">Mappen als logische gegevenssets</span><span class="sxs-lookup"><span data-stu-id="1abc8-110">Directories as logical data sets</span></span>
<span data-ttu-id="1abc8-111">Een algemene patroon voor het ordenen van grote gegevensbronnen is tootreat mappen als logische gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="1abc8-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="1abc8-112">Op het hoogste niveau mappen zijn gebruikte toodefine een gegevensset terwijl submappen Definieer partities en Hallo-bestanden die ze bevatten opslaan Hallo gegevens zelf.</span><span class="sxs-lookup"><span data-stu-id="1abc8-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="1abc8-113">Een voorbeeld van dit patroon is mogelijk:</span><span class="sxs-lookup"><span data-stu-id="1abc8-113">An example of this pattern might be:</span></span>

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

<span data-ttu-id="1abc8-114">In dit voorbeeld vertegenwoordigen vehicle_maintenance_events en location_tracking_events logische gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="1abc8-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="1abc8-115">Elk van deze mappen bevat gegevensbestanden die zijn ingedeeld op jaar en maand in submappen.</span><span class="sxs-lookup"><span data-stu-id="1abc8-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="1abc8-116">Elk van deze mappen zich mogelijk honderden of duizenden bestanden.</span><span class="sxs-lookup"><span data-stu-id="1abc8-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="1abc8-117">In dit patroon registratie van afzonderlijke bestanden met **Azure Data Catalog** waarschijnlijk niet logisch.</span><span class="sxs-lookup"><span data-stu-id="1abc8-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="1abc8-118">In plaats daarvan registreert Hallo-mappen die Hallo gegevenssets die worden zinvolle toohello gebruikers werken met gegevens Hallo vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="1abc8-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="1abc8-119">Verwijzing naar gegevensbestanden</span><span class="sxs-lookup"><span data-stu-id="1abc8-119">Reference data files</span></span>
<span data-ttu-id="1abc8-120">Een aanvullende patroon is sets van verwijzingsgegevens toostore als afzonderlijke bestanden.</span><span class="sxs-lookup"><span data-stu-id="1abc8-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="1abc8-121">Deze gegevenssets kunnen worden beschouwd als 'kleine' Hallo-zijde van big data en zijn vaak vergelijkbare toodimensions in een model analytische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1abc8-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="1abc8-122">Verwijzing naar gegevensbestanden bevatten records die gebruikt tooprovide context voor bulksgewijs Hallo van gegevensbestanden Hallo elders in Hallo big data-archief opgeslagen zijn.</span><span class="sxs-lookup"><span data-stu-id="1abc8-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="1abc8-123">Een voorbeeld van dit patroon is mogelijk:</span><span class="sxs-lookup"><span data-stu-id="1abc8-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="1abc8-124">Wanneer een analist of gegevens wetenschappelijk met gegevens in grotere mapstructuren Hallo hello werkt, kunnen Hallo-gegevens in deze bestanden verwijzing gebruikte tooprovide meer informatie gedetailleerde voor entiteiten die zijn bedoeld tooonly op naam of ID in grotere Hallo-gegevens worden set.</span><span class="sxs-lookup"><span data-stu-id="1abc8-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="1abc8-125">In dit patroon is het zinvol tooregister Hallo afzonderlijke verwijzing gegevensbestanden met **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="1abc8-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="1abc8-126">Elk bestand vertegenwoordigt een set gegevens en elkaar kan worden aangetekend en afzonderlijk gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="1abc8-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="1abc8-127">Alternatieve patronen</span><span class="sxs-lookup"><span data-stu-id="1abc8-127">Alternate patterns</span></span>
<span data-ttu-id="1abc8-128">Hallo patronen die zijn beschreven in voorgaande sectie Hallo zijn twee manieren die een big data store kan worden georganiseerd, maar elke implementatie verschilt.</span><span class="sxs-lookup"><span data-stu-id="1abc8-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="1abc8-129">Ongeacht hoe uw gegevensbronnen zijn gestructureerd, bij het registreren van gegevensbronnen met big **Azure Data Catalog**, ligt de nadruk op het registreren van Hallo bestanden en mappen die vertegenwoordigen gegevenssets Hallo van waarde tooothers binnen uw de organisatie.</span><span class="sxs-lookup"><span data-stu-id="1abc8-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="1abc8-130">Registratie van alle bestanden en mappen kan bruikbaar blijft Hallo-catalogus, waardoor het moeilijker voor gebruikers toofind die ze nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="1abc8-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="1abc8-131">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="1abc8-131">Summary</span></span>
<span data-ttu-id="1abc8-132">Registreren van gegevensbronnen met **Azure Data Catalog** maakt u ze eenvoudiger toodiscover en begrijpen.</span><span class="sxs-lookup"><span data-stu-id="1abc8-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="1abc8-133">Door te registreren en aantekeningen Hallo big data-bestanden en mappen die logische gegevenssets vertegenwoordigen, kunt u gebruikers zoeken en Hallo big-gegevensbronnen die ze nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="1abc8-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
