---
title: een Machine Learning-webservice vanuit Excel aaaConsume | Microsoft Docs
description: Een Azure Machine Learning-webservice vanuit Excel gebruiken
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="cadf0-103">Een Azure Machine Learning-webservice gebruiken vanuit Excel</span><span class="sxs-lookup"><span data-stu-id="cadf0-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="cadf0-104">Azure Machine Learning Studio maakt het eenvoudig toocall webservices rechtstreeks vanuit Excel zonder Hallo moet toowrite code.</span><span class="sxs-lookup"><span data-stu-id="cadf0-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="cadf0-105">Als u Excel 2013 (of hoger) of Excel Online gebruikt, wordt aangeraden dat u Excel Hallo [Excel-invoegtoepassing](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="cadf0-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="cadf0-106">Stappen</span><span class="sxs-lookup"><span data-stu-id="cadf0-106">Steps</span></span>
<span data-ttu-id="cadf0-107">Een webservice publiceert.</span><span class="sxs-lookup"><span data-stu-id="cadf0-107">Publish a web service.</span></span> <span data-ttu-id="cadf0-108">[Deze pagina](machine-learning-walkthrough-5-publish-web-service.md) wordt uitgelegd hoe toodo deze.</span><span class="sxs-lookup"><span data-stu-id="cadf0-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="cadf0-109">Hallo Excel-werkmap functie is momenteel alleen ondersteund voor de aanvraag/antwoord-services die één uitvoer (dat wil zeggen, een enkel scoreprofiel label).</span><span class="sxs-lookup"><span data-stu-id="cadf0-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="cadf0-110">Zodra u een webservice hebt, klik op Hallo **WEBSERVICES** sectie aan de linkerkant Hallo van Hallo studio, en selecteer vervolgens Hallo web service tooconsume in Excel.</span><span class="sxs-lookup"><span data-stu-id="cadf0-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="cadf0-111">**Klassieke webservice**</span><span class="sxs-lookup"><span data-stu-id="cadf0-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="cadf0-112">Op Hallo **DASHBOARD** tabblad voor Hallo-webservice een rij voor Hallo is **aanvragen/reacties** service.</span><span class="sxs-lookup"><span data-stu-id="cadf0-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="cadf0-113">Als deze service één uitvoer heeft, ziet u Hallo **Excel-werkmap downloaden** koppeling in die rij.</span><span class="sxs-lookup"><span data-stu-id="cadf0-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="cadf0-114">Klik op **Excel-werkmap downloaden**.</span><span class="sxs-lookup"><span data-stu-id="cadf0-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="cadf0-115">**Nieuwe webservice**</span><span class="sxs-lookup"><span data-stu-id="cadf0-115">**New Web Service**</span></span>

1. <span data-ttu-id="cadf0-116">Selecteer in hello Azure Machine Learning-webservice portal **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="cadf0-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="cadf0-117">Hallo verbruiken in op pagina Hallo **Web-verbruik serviceopties** sectie, klikt u op Hallo Excel-pictogram.</span><span class="sxs-lookup"><span data-stu-id="cadf0-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="cadf0-118">**Hallo werkmap**</span><span class="sxs-lookup"><span data-stu-id="cadf0-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="cadf0-119">Open Hallo-werkmap.</span><span class="sxs-lookup"><span data-stu-id="cadf0-119">Open hello workbook.</span></span>
2. <span data-ttu-id="cadf0-120">Er verschijnt een beveiligingswaarschuwing; Klik op Hallo **bewerken inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="cadf0-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="cadf0-121">Een beveiligingswaarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cadf0-121">A Security Warning appears.</span></span> <span data-ttu-id="cadf0-122">Klik op Hallo **inhoud inschakelen** knop toorun macro's in het werkblad.</span><span class="sxs-lookup"><span data-stu-id="cadf0-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="cadf0-123">Zodra de macro's zijn ingeschakeld, wordt een tabel wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="cadf0-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="cadf0-124">Kolommen in blauw zijn vereist als invoer in Hallo RRS-webservice of **PARAMETERS**.</span><span class="sxs-lookup"><span data-stu-id="cadf0-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="cadf0-125">Houd er rekening mee Hallo uitvoer Hallo RRS-service, **VOORSPELDE waarden** in groen.</span><span class="sxs-lookup"><span data-stu-id="cadf0-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="cadf0-126">Wanneer alle kolommen voor een bepaalde rij zijn ingevuld, Hallo werkmap automatisch Hallo score berekenen voor API-aanroepen en Hallo berekend resultaten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cadf0-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="cadf0-127">tooscore meer dan een rij, voorspelde opvulling Hallo tweede rij met gegevens en Hallo waarden worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="cadf0-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="cadf0-128">U kunt zelfs meerdere rijen in één keer plakken.</span><span class="sxs-lookup"><span data-stu-id="cadf0-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="cadf0-129">U Hallo Excel-functies (grafieken, power-kaart, voorwaardelijke opmaak, enz.) kunt gebruiken met Hallo voorspelde waarden toohelp Hallo gegevens visualiseren.</span><span class="sxs-lookup"><span data-stu-id="cadf0-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="cadf0-130">Delen van uw werkmap</span><span class="sxs-lookup"><span data-stu-id="cadf0-130">Sharing your workbook</span></span>
<span data-ttu-id="cadf0-131">Voor Hallo macro's toowork, moet uw API-sleutel deel uitmaken van Hallo werkblad.</span><span class="sxs-lookup"><span data-stu-id="cadf0-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="cadf0-132">Dat betekent dat u alleen met entiteiten/personen die u vertrouwt Hallo werkmap moet delen.</span><span class="sxs-lookup"><span data-stu-id="cadf0-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="cadf0-133">Automatische updates</span><span class="sxs-lookup"><span data-stu-id="cadf0-133">Automatic updates</span></span>
<span data-ttu-id="cadf0-134">In deze situaties wordt een RRS-aanroep uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="cadf0-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="cadf0-135">Hallo eerst een rij heeft de inhoud in alle bijbehorende **PARAMETERS**</span><span class="sxs-lookup"><span data-stu-id="cadf0-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="cadf0-136">Telkens wanneer u een van de Hallo **PARAMETERS** wijzigingen in een rij die alle waren bijbehorende **PARAMETERS** ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="cadf0-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
