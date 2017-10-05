---
title: Gegevensbronnen documenteren | Microsoft Docs
description: Hoe kan ik artikel documenteren gegevensassets in Azure Data Catalog is gemarkeerd.
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
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="d5922-103">Gegevensbronnen documenteren</span><span class="sxs-lookup"><span data-stu-id="d5922-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="d5922-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="d5922-104">Introduction</span></span>
<span data-ttu-id="d5922-105">**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert.</span><span class="sxs-lookup"><span data-stu-id="d5922-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="d5922-106">Met andere woorden, **Azure Data Catalog** helpen bij het detecteren, mensen *begrijpen*, gegevensbronnen, en gebruik helpt organisaties bij het ophalen van meerwaarde van hun bestaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="d5922-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="d5922-107">Wanneer een gegevensbron is geregistreerd met **Azure Data Catalog**, de metagegevens wordt gekopieerd en geïndexeerd door de service, maar het artikel er eindigt niet.</span><span class="sxs-lookup"><span data-stu-id="d5922-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="d5922-108">**Azure Data Catalog** ook kunnen gebruikers zich hebben hun eigen volledige documentatie die wordt beschreven en het gebruik en algemene scenario's voor de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="d5922-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="d5922-109">In [aantekeningen toevoegen aan gegevensbronnen](data-catalog-how-to-annotate.md), leert u dat deskundigen die kennen van de gegevensbron kunnen aantekeningen toevoegen aan deze met tags en een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="d5922-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="d5922-110">De **Azure Data Catalog** portal bevat een uitgebreide teksteditor zodat gebruikers kunnen volledig Documenteer gegevensassets en containers.</span><span class="sxs-lookup"><span data-stu-id="d5922-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="d5922-111">De editor bevat alinea-opmaak, zoals koppen, tekstopmaak opsommingstekens, genummerde lijsten en tabellen.</span><span class="sxs-lookup"><span data-stu-id="d5922-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="d5922-112">Labels en beschrijvingen zijn ideaal voor eenvoudige aantekeningen.</span><span class="sxs-lookup"><span data-stu-id="d5922-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="d5922-113">Een expert kan echter om te helpen gegevensgebruikers meer informatie over het gebruik van een gegevensbron en zakelijke scenario's voor een gegevensbron, bieden volledige, gedetailleerde documentatie.</span><span class="sxs-lookup"><span data-stu-id="d5922-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="d5922-114">Het is gemakkelijk om vast te leggen van een gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="d5922-114">It's easy to document a data source.</span></span> <span data-ttu-id="d5922-115">Selecteer een gegevensasset of de container en kies **documentatie**.</span><span class="sxs-lookup"><span data-stu-id="d5922-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="d5922-116">Gegevensassets documenteren</span><span class="sxs-lookup"><span data-stu-id="d5922-116">Documenting data assets</span></span>
<span data-ttu-id="d5922-117">Het voordeel van **Azure Data Catalog** documentatie kunt u uw Data Catalog gebruiken als een opslagplaats voor inhoud voor het maken van volledige sprekersnotities van uw gegevensassets.</span><span class="sxs-lookup"><span data-stu-id="d5922-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="d5922-118">Hier vindt u gedetailleerde inhoud waarin wordt beschreven containers en tabellen.</span><span class="sxs-lookup"><span data-stu-id="d5922-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="d5922-119">Als u al inhoud in een andere opslagplaats voor inhoud, zoals SharePoint of een bestandsshare, kunt u toevoegen aan de asset documentatie koppelingen om te verwijzen naar deze bestaande inhoud.</span><span class="sxs-lookup"><span data-stu-id="d5922-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="d5922-120">Deze functie kunt uw bestaande documenten beter kunnen worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="d5922-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="d5922-121">Documentatie is niet opgenomen in de search-index.</span><span class="sxs-lookup"><span data-stu-id="d5922-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="d5922-122">Het niveau van documentatie kan variëren van met een beschrijving van de kenmerken en de waarde van een container van de asset gegevens voor een gedetailleerde beschrijving van tabelschema binnen een container.</span><span class="sxs-lookup"><span data-stu-id="d5922-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="d5922-123">Het niveau van documentatie moet worden bepaald door de behoeften van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="d5922-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="d5922-124">Maar in het algemeen zijn hier enkele voordelen en nadelen van gegevensassets documenteren:</span><span class="sxs-lookup"><span data-stu-id="d5922-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="d5922-125">Een container-document: de inhoud is op één plaats, maar mogelijk niet over de benodigde informatie voor gebruikers om te beslissen.</span><span class="sxs-lookup"><span data-stu-id="d5922-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="d5922-126">Alleen de tabellen-document: inhoud is specifiek voor dat object, maar uw gebruikers beschikken over meerdere locaties voor documenten.</span><span class="sxs-lookup"><span data-stu-id="d5922-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="d5922-127">Documenteer containers en tabellen: meest uitgebreide benadering, maar mogelijk sprake meer onderhoud van de documenten.</span><span class="sxs-lookup"><span data-stu-id="d5922-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="d5922-128">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d5922-128">Summary</span></span>
<span data-ttu-id="d5922-129">Gegevensbronnen met documenteren **Azure Data Catalog** sprekersnotities over uw gegevensassets zo gedetailleerd naar wens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="d5922-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="d5922-130">U kunt met behulp van koppelingen koppelen aan inhoud die is opgeslagen in een bestaande opslagplaats voor inhoud, een combinatie van uw bestaande documenten en gegevensassets.</span><span class="sxs-lookup"><span data-stu-id="d5922-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="d5922-131">Wanneer uw gebruikers juiste gegevensassets detecteren, kunnen ze een volledige set van documentatie hebben.</span><span class="sxs-lookup"><span data-stu-id="d5922-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
