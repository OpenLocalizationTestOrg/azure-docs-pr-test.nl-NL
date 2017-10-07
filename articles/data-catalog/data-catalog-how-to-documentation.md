---
title: aaaHow toodocument gegevensbronnen | Microsoft Docs
description: Hoe tooarticle markeren hoe toodocument gegevensassets in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="2500f-103">Gegevensbronnen documenteren</span><span class="sxs-lookup"><span data-stu-id="2500f-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="2500f-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="2500f-104">Introduction</span></span>
<span data-ttu-id="2500f-105">**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert.</span><span class="sxs-lookup"><span data-stu-id="2500f-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="2500f-106">Met andere woorden, **Azure Data Catalog** helpen bij het detecteren, mensen *begrijpen*, en gebruik van gegevensbronnen en organisaties tooget meer van hun bestaande gegevens waarde te helpen.</span><span class="sxs-lookup"><span data-stu-id="2500f-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="2500f-107">Wanneer een gegevensbron is geregistreerd met **Azure Data Catalog**, de metagegevens wordt gekopieerd en geïndexeerd door Hallo-service, maar Hallo verhaal er eindigt niet.</span><span class="sxs-lookup"><span data-stu-id="2500f-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="2500f-108">**Azure Data Catalog** ook hun eigen volledige documentatie die wordt beschreven en Hallo gebruiks- en algemene scenario's voor de gegevensbron Hallo kunnen gebruikers tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2500f-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="2500f-109">In [hoe gegevensbronnen tooannotate](data-catalog-how-to-annotate.md), leert u dat deskundigen die Hallo-gegevensbron kennen kunnen aantekeningen toevoegen aan deze met tags en een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="2500f-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="2500f-110">Hallo **Azure Data Catalog** portal bevat een uitgebreide teksteditor zodat gebruikers kunnen volledig Documenteer gegevensassets en containers.</span><span class="sxs-lookup"><span data-stu-id="2500f-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="2500f-111">Hallo-editor bevat alinea-opmaak, zoals kopteksten, tekstopmaak, lijsten met opsommingstekens, genummerde lijsten en tabellen.</span><span class="sxs-lookup"><span data-stu-id="2500f-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="2500f-112">Labels en beschrijvingen zijn ideaal voor eenvoudige aantekeningen.</span><span class="sxs-lookup"><span data-stu-id="2500f-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="2500f-113">Echter toohelp gegevensgebruikers Hallo gebruik van een gegevensbron beter te begrijpen en zakelijke scenario's voor een gegevensbron, een expert volledige, gedetailleerde documentatie kunnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="2500f-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="2500f-114">Het is gemakkelijk toodocument een gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="2500f-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="2500f-115">Selecteer een gegevensasset of de container en kies **documentatie**.</span><span class="sxs-lookup"><span data-stu-id="2500f-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="2500f-116">Gegevensassets documenteren</span><span class="sxs-lookup"><span data-stu-id="2500f-116">Documenting data assets</span></span>
<span data-ttu-id="2500f-117">Hallo voordeel van **Azure Data Catalog** documentatie kunt u toouse uw Data Catalog als een opslagplaats voor inhoud toocreate voltooid sprekersnotities van uw gegevensassets.</span><span class="sxs-lookup"><span data-stu-id="2500f-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="2500f-118">Hier vindt u gedetailleerde inhoud waarin wordt beschreven containers en tabellen.</span><span class="sxs-lookup"><span data-stu-id="2500f-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="2500f-119">Als u al inhoud in een andere opslagplaats voor inhoud, zoals SharePoint of een bestandsshare, kunt u deze bestaande inhoud toohello asset documentatie koppelingen tooreference toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2500f-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="2500f-120">Deze functie kunt uw bestaande documenten beter kunnen worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="2500f-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="2500f-121">Documentatie is niet opgenomen in de search-index.</span><span class="sxs-lookup"><span data-stu-id="2500f-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="2500f-122">Hallo niveau van documentatie tussen beschrijven Hallo kenmerken en de waarde van een data asset container tooa gedetailleerde beschrijving van tabelschema binnen een container.</span><span class="sxs-lookup"><span data-stu-id="2500f-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="2500f-123">Hallo-niveau van documentatie moet worden aangestuurd door uw bedrijfsbehoeften.</span><span class="sxs-lookup"><span data-stu-id="2500f-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="2500f-124">Maar in het algemeen zijn hier enkele voordelen en nadelen van gegevensassets documenteren:</span><span class="sxs-lookup"><span data-stu-id="2500f-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="2500f-125">Een container-document: alle Hallo-inhoud is op één plaats, maar mogelijk ontbreken nodig de gegevens voor gebruikers toomake een gefundeerde beslissing nemen.</span><span class="sxs-lookup"><span data-stu-id="2500f-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="2500f-126">Documenteer NET Hallo tabellen: inhoud is specifieke toothat object, maar uw gebruikers beschikken over meerdere locaties voor documenten.</span><span class="sxs-lookup"><span data-stu-id="2500f-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="2500f-127">Documenteer containers en tabellen: meest uitgebreide benadering, maar mogelijk sprake meer onderhoud van Hallo documenten.</span><span class="sxs-lookup"><span data-stu-id="2500f-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="2500f-128">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="2500f-128">Summary</span></span>
<span data-ttu-id="2500f-129">Gegevensbronnen met documenteren **Azure Data Catalog** sprekersnotities over uw gegevensassets zo gedetailleerd naar wens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="2500f-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="2500f-130">U kunt via koppelingen toocontent opgeslagen in een bestaande opslagplaats voor inhoud, een combinatie van uw bestaande documenten en gegevensassets koppelen.</span><span class="sxs-lookup"><span data-stu-id="2500f-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="2500f-131">Wanneer uw gebruikers juiste gegevensassets detecteren, kunnen ze een volledige set van documentatie hebben.</span><span class="sxs-lookup"><span data-stu-id="2500f-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
