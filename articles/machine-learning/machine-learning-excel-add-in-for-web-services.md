---
title: aaaExcel-invoegtoepassing voor Machine Learning-webservices | Microsoft Docs
description: Hoe toouse Azure Machine Learning Web services rechtstreeks in Excel zonder een code te schrijven.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="a015e-103">Excel-invoegtoepassing voor Azure Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="a015e-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="a015e-104">Excel kunt u eenvoudig toocall webservices rechtstreeks zonder Hallo moet toowrite code.</span><span class="sxs-lookup"><span data-stu-id="a015e-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="a015e-105">Stappen tooUse een bestaande webservice in Hallo werkmap</span><span class="sxs-lookup"><span data-stu-id="a015e-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="a015e-106">Open Hallo [voorbeeld-Excel-bestand](http://aka.ms/amlexcel-sample-2), die bevat Hallo Excel-invoegtoepassing en gegevens over passagiers op Hallo Titanic.</span><span class="sxs-lookup"><span data-stu-id="a015e-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="a015e-107">Hallo-webservice kiezen door erop te klikken-' Titanic nagelaten manier (Excel-invoegtoepassing voorbeeld) [Score] ' in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a015e-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![-Webservice selecteren][01]
3. <span data-ttu-id="a015e-109">Hiermee gaat u toohello **Predict** sectie.</span><span class="sxs-lookup"><span data-stu-id="a015e-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="a015e-110">Deze werkmap bevat al de voorbeeldgegevens, maar voor een lege werkmap kunt u Selecteer een cel in Excel en klik op **voorbeeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="a015e-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="a015e-111">Hallo-gegevens met kopteksten selecteren en klik op Hallo invoergegevens bereik pictogram.</span><span class="sxs-lookup"><span data-stu-id="a015e-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="a015e-112">Zorg ervoor dat Hallo 'Mijn gegevens heeft headers' selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a015e-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="a015e-113">Onder **uitvoer**, Voer Hallo cel getal waar u hier uitvoer toobe, bijvoorbeeld 'H1' Hallo.</span><span class="sxs-lookup"><span data-stu-id="a015e-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="a015e-114">Klik op **voorspellen**.</span><span class="sxs-lookup"><span data-stu-id="a015e-114">Click **Predict**.</span></span>
   
    ![Sectie voorspellen][02]

<span data-ttu-id="a015e-116">Implementeer een webservice of een bestaande webservice gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a015e-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="a015e-117">Zie voor meer informatie over het implementeren van een webservice [scenario stap 5: hello Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="a015e-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="a015e-118">Hallo-API-sleutel voor uw webservice ophalen.</span><span class="sxs-lookup"><span data-stu-id="a015e-118">Get hello API key for your web service.</span></span> <span data-ttu-id="a015e-119">Wanneer u uitvoeren met deze actie is afhankelijk van of u een klassieke Machine Learning-webservice van een nieuwe Machine-Learning-webservice gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="a015e-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="a015e-120">**Een klassieke webservice gebruiken**</span><span class="sxs-lookup"><span data-stu-id="a015e-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="a015e-121">Klik op Hallo in Machine Learning Studio **WEBSERVICES** sectie in het linkerdeelvenster Hallo en selecteer vervolgens Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="a015e-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Studio, selecteer een webservice][04]
2. <span data-ttu-id="a015e-123">Kopieer Hallo API-sleutel voor Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="a015e-123">Copy hello API key for hello web service.</span></span>
   
    ![Studio-API-sleutel][05]
3. <span data-ttu-id="a015e-125">Op Hallo **DASHBOARD** voor Hallo-webservice en klik op Hallo **aanvragen/reacties** koppeling.</span><span class="sxs-lookup"><span data-stu-id="a015e-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="a015e-126">Zoek naar Hallo **aanvraag-URI** sectie.</span><span class="sxs-lookup"><span data-stu-id="a015e-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="a015e-127">Kopieer en sla Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="a015e-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="a015e-128">Het is nu mogelijk toosign in Hallo [Azure Machine Learning-webservices](https://services.azureml.net) portal tooobtain Hallo API-sleutel voor een klassieke Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="a015e-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="a015e-129">**Een nieuwe webservice gebruiken**</span><span class="sxs-lookup"><span data-stu-id="a015e-129">**Use a New web service**</span></span>

1. <span data-ttu-id="a015e-130">In Hallo [Azure Machine Learning-webservices](https://services.azureml.net) en klik op **webservices**, selecteer vervolgens uw webservice.</span><span class="sxs-lookup"><span data-stu-id="a015e-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="a015e-131">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="a015e-131">Click **Consume**.</span></span>
3. <span data-ttu-id="a015e-132">Zoek naar Hallo **Basic verbruik info** sectie.</span><span class="sxs-lookup"><span data-stu-id="a015e-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="a015e-133">Kopiëren en opslaan van Hallo **primaire sleutel** en Hallo **aanvragen en antwoorden** URL.</span><span class="sxs-lookup"><span data-stu-id="a015e-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="a015e-134">TooAdd stappen een nieuwe webservice</span><span class="sxs-lookup"><span data-stu-id="a015e-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="a015e-135">Implementeer een webservice of een bestaande webservice gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a015e-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="a015e-136">Zie voor meer informatie over het implementeren van een webservice [scenario stap 5: hello Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="a015e-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="a015e-137">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="a015e-137">Click **Consume**.</span></span>
3. <span data-ttu-id="a015e-138">Zoek naar Hallo **Basic verbruik info** sectie.</span><span class="sxs-lookup"><span data-stu-id="a015e-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="a015e-139">Kopiëren en opslaan van Hallo **primaire sleutel** en Hallo **aanvragen en antwoorden** URL.</span><span class="sxs-lookup"><span data-stu-id="a015e-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="a015e-140">Ga in Excel, toohello **webservices** sectie (als u in Hallo **Predict** sectie, klikt u op Hallo pijl naar links toogo toohello lijst met web-services).</span><span class="sxs-lookup"><span data-stu-id="a015e-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Ga tooWeb service selecteren][03]
5. <span data-ttu-id="a015e-142">Klik op **-webservice toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a015e-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="a015e-143">Plak Hallo-URL in Excel-invoegtoepassing tekstvak met het label Hallo **URL**.</span><span class="sxs-lookup"><span data-stu-id="a015e-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="a015e-144">Plakken Hallo API/primaire sleutel in Hallo tekstvak met het label **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="a015e-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="a015e-145">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="a015e-145">Click **Add**.</span></span>
   
    ![URL en API-sleutel voor een klassieke webservice.][06]
9. <span data-ttu-id="a015e-147">toouse hello webservice Hallo voorafgaand aan de instructies volgen, "Stappen voor het tooUse een bestaande web Service."</span><span class="sxs-lookup"><span data-stu-id="a015e-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="a015e-148">Delen van uw werkmap</span><span class="sxs-lookup"><span data-stu-id="a015e-148">Sharing Your Workbook</span></span>
<span data-ttu-id="a015e-149">Als u de werkmap opslaan, wordt ook Hallo API/primaire sleutel voor het Hallo-webservices die u hebt toegevoegd opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a015e-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="a015e-150">Dit betekent dat u moet Hallo werkmap alleen delen met personen die u vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="a015e-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="a015e-151">Vragen te stellen in Hallo volgende sectie Opmerking of op onze [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="a015e-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
