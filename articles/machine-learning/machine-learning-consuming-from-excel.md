---
title: Een Machine Learning-webservice vanuit Excel gebruiken | Microsoft Docs
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
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="de650-103">Een Azure Machine Learning-webservice gebruiken vanuit Excel</span><span class="sxs-lookup"><span data-stu-id="de650-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="de650-104">Azure Machine Learning Studio kunt gemakkelijk aanroepen van webservices rechtstreeks vanuit Excel zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="de650-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="de650-105">Als u Excel 2013 (of hoger) of Excel Online gebruikt, wordt aangeraden dat u de Excel [Excel-invoegtoepassing](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="de650-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="de650-106">Stappen</span><span class="sxs-lookup"><span data-stu-id="de650-106">Steps</span></span>
<span data-ttu-id="de650-107">Een webservice publiceert.</span><span class="sxs-lookup"><span data-stu-id="de650-107">Publish a web service.</span></span> <span data-ttu-id="de650-108">[Deze pagina](machine-learning-walkthrough-5-publish-web-service.md) wordt uitgelegd hoe u dit doen.</span><span class="sxs-lookup"><span data-stu-id="de650-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="de650-109">De functie van de Excel-werkmap is momenteel alleen ondersteund voor de aanvraag/antwoord-services die één uitvoer (dat wil zeggen, een enkel scoreprofiel label).</span><span class="sxs-lookup"><span data-stu-id="de650-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="de650-110">Zodra u een webservice hebt, klikt u op in de **WEBSERVICES** sectie aan de linkerkant van de studio en selecteer vervolgens de web-service gebruiken vanuit Excel.</span><span class="sxs-lookup"><span data-stu-id="de650-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="de650-111">**Klassieke webservice**</span><span class="sxs-lookup"><span data-stu-id="de650-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="de650-112">Op de **DASHBOARD** tabblad voor de webservice is een rij voor de **aanvragen/reacties** service.</span><span class="sxs-lookup"><span data-stu-id="de650-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="de650-113">Als deze service één uitvoer heeft, ziet u de **Excel-werkmap downloaden** koppeling in die rij.</span><span class="sxs-lookup"><span data-stu-id="de650-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="de650-114">Klik op **Excel-werkmap downloaden**.</span><span class="sxs-lookup"><span data-stu-id="de650-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="de650-115">**Nieuwe webservice**</span><span class="sxs-lookup"><span data-stu-id="de650-115">**New Web Service**</span></span>

1. <span data-ttu-id="de650-116">Selecteer in de portal voor Azure Machine Learning-webservice **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="de650-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="de650-117">Op de pagina verbruiken in de **Web-verbruik serviceopties** sectie, klikt u op het Excel-pictogram.</span><span class="sxs-lookup"><span data-stu-id="de650-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="de650-118">**Met behulp van de werkmap**</span><span class="sxs-lookup"><span data-stu-id="de650-118">**Using the workbook**</span></span>

1. <span data-ttu-id="de650-119">Open de werkmap.</span><span class="sxs-lookup"><span data-stu-id="de650-119">Open the workbook.</span></span>
2. <span data-ttu-id="de650-120">Er verschijnt een beveiligingswaarschuwing; Klik op de **bewerken inschakelen** knop.</span><span class="sxs-lookup"><span data-stu-id="de650-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="de650-121">Een beveiligingswaarschuwing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="de650-121">A Security Warning appears.</span></span> <span data-ttu-id="de650-122">Klik op de **inhoud inschakelen** knop voor het uitvoeren van macro's in het werkblad.</span><span class="sxs-lookup"><span data-stu-id="de650-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="de650-123">Zodra de macro's zijn ingeschakeld, wordt een tabel wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="de650-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="de650-124">Kolommen in blauw zijn vereist als invoer in de webservice RRS of **PARAMETERS**.</span><span class="sxs-lookup"><span data-stu-id="de650-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="de650-125">De uitvoer van de service RRS **VOORSPELDE waarden** in groen.</span><span class="sxs-lookup"><span data-stu-id="de650-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="de650-126">Wanneer alle kolommen voor een bepaalde rij gevuld zijn, de werkmap automatisch de score API aanroept en de scored resultaten worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="de650-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="de650-127">Als u wilt beoordelen meer dan één rij, opvulling van de tweede rij met gegevens en de voorspelde waarden worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="de650-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="de650-128">U kunt zelfs meerdere rijen in één keer plakken.</span><span class="sxs-lookup"><span data-stu-id="de650-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="de650-129">U kunt de Excel-functies (grafieken, power-kaart, voorwaardelijke opmaak, enz.) met de voorspelde waarden gebruiken om u te helpen de gegevens visualiseren.</span><span class="sxs-lookup"><span data-stu-id="de650-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="de650-130">Delen van uw werkmap</span><span class="sxs-lookup"><span data-stu-id="de650-130">Sharing your workbook</span></span>
<span data-ttu-id="de650-131">Voor de macro's werken, moet uw API-sleutel deel uitmaken van het werkblad.</span><span class="sxs-lookup"><span data-stu-id="de650-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="de650-132">Dat betekent dat u de werkmap moet delen alleen met entiteiten/personen die u vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="de650-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="de650-133">Automatische updates</span><span class="sxs-lookup"><span data-stu-id="de650-133">Automatic updates</span></span>
<span data-ttu-id="de650-134">In deze situaties wordt een RRS-aanroep uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="de650-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="de650-135">De eerste keer dat een rij bevat inhoud in alle bijbehorende **PARAMETERS**</span><span class="sxs-lookup"><span data-stu-id="de650-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="de650-136">Telkens wanneer u een van de **PARAMETERS** wijzigingen in een rij die alle waren bijbehorende **PARAMETERS** ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="de650-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
