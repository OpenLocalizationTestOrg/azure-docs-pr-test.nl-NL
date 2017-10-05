---
title: Excel-invoegtoepassing voor Machine Learning-webservices | Microsoft Docs
description: Het gebruik van Azure Machine Learning-webservices rechtstreeks in Excel zonder een code te schrijven.
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
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="4eb06-103">Excel-invoegtoepassing voor Azure Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="4eb06-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="4eb06-104">Excel kunt u gemakkelijk om aan te roepen webservices rechtstreeks zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="4eb06-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="4eb06-105">Stappen voor het gebruik van een bestaande webservice in de werkmap</span><span class="sxs-lookup"><span data-stu-id="4eb06-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="4eb06-106">Open de [voorbeeld-Excel-bestand](http://aka.ms/amlexcel-sample-2), die de Excel-invoegtoepassing en de gegevens over passagiers op de Titanic bevat.</span><span class="sxs-lookup"><span data-stu-id="4eb06-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="4eb06-107">De webservice kiezen door erop te klikken-' Titanic nagelaten manier (Excel-invoegtoepassing voorbeeld) [Score] ' in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4eb06-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![-Webservice selecteren][01]
3. <span data-ttu-id="4eb06-109">Hiermee gaat u naar de **Predict** sectie.</span><span class="sxs-lookup"><span data-stu-id="4eb06-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="4eb06-110">Deze werkmap bevat al de voorbeeldgegevens, maar voor een lege werkmap kunt u Selecteer een cel in Excel en klik op **voorbeeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="4eb06-111">Selecteer de gegevens met kopteksten en klik op het pictogram van invoergegevens bereik.</span><span class="sxs-lookup"><span data-stu-id="4eb06-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="4eb06-112">Zorg ervoor dat het selectievakje 'Mijn gegevens heeft headers' is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4eb06-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="4eb06-113">Onder **uitvoer**, voer het celnummer waar u de uitvoer te zijn, bijvoorbeeld 'H1' hier.</span><span class="sxs-lookup"><span data-stu-id="4eb06-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="4eb06-114">Klik op **voorspellen**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-114">Click **Predict**.</span></span>
   
    ![Sectie voorspellen][02]

<span data-ttu-id="4eb06-116">Implementeer een webservice of een bestaande webservice gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4eb06-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="4eb06-117">Zie voor meer informatie over het implementeren van een webservice [scenario stap 5: de Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4eb06-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="4eb06-118">De API-sleutel voor uw webservice ophalen.</span><span class="sxs-lookup"><span data-stu-id="4eb06-118">Get the API key for your web service.</span></span> <span data-ttu-id="4eb06-119">Wanneer u uitvoeren met deze actie is afhankelijk van of u een klassieke Machine Learning-webservice van een nieuwe Machine-Learning-webservice gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="4eb06-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="4eb06-120">**Een klassieke webservice gebruiken**</span><span class="sxs-lookup"><span data-stu-id="4eb06-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="4eb06-121">In Machine Learning Studio, klikt u op de **WEBSERVICES** sectie in het linkerdeelvenster en selecteer vervolgens de webservice.</span><span class="sxs-lookup"><span data-stu-id="4eb06-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Studio, selecteer een webservice][04]
2. <span data-ttu-id="4eb06-123">Kopieer de API-sleutel voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="4eb06-123">Copy the API key for the web service.</span></span>
   
    ![Studio-API-sleutel][05]
3. <span data-ttu-id="4eb06-125">Op de **DASHBOARD** voor de webservice en klik op de **aanvragen/reacties** koppeling.</span><span class="sxs-lookup"><span data-stu-id="4eb06-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="4eb06-126">Zoek naar de **aanvraag-URI** sectie.</span><span class="sxs-lookup"><span data-stu-id="4eb06-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="4eb06-127">Kopieer en sla de URL.</span><span class="sxs-lookup"><span data-stu-id="4eb06-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="4eb06-128">Het is nu mogelijk om aan te melden bij de [Azure Machine Learning-webservices](https://services.azureml.net) portal om op te halen van de API-sleutel voor een klassieke Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="4eb06-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="4eb06-129">**Een nieuwe webservice gebruiken**</span><span class="sxs-lookup"><span data-stu-id="4eb06-129">**Use a New web service**</span></span>

1. <span data-ttu-id="4eb06-130">In de [Azure Machine Learning-webservices](https://services.azureml.net) en klik op **webservices**, selecteer vervolgens uw webservice.</span><span class="sxs-lookup"><span data-stu-id="4eb06-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="4eb06-131">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-131">Click **Consume**.</span></span>
3. <span data-ttu-id="4eb06-132">Zoek naar de **Basic verbruik info** sectie.</span><span class="sxs-lookup"><span data-stu-id="4eb06-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="4eb06-133">Kopieer en sla de **primaire sleutel** en de **aanvragen en antwoorden** URL.</span><span class="sxs-lookup"><span data-stu-id="4eb06-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="4eb06-134">Stappen voor een nieuwe webservice toevoegen</span><span class="sxs-lookup"><span data-stu-id="4eb06-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="4eb06-135">Implementeer een webservice of een bestaande webservice gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4eb06-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="4eb06-136">Zie voor meer informatie over het implementeren van een webservice [scenario stap 5: de Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="4eb06-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="4eb06-137">Klik op **verbruiken**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-137">Click **Consume**.</span></span>
3. <span data-ttu-id="4eb06-138">Zoek naar de **Basic verbruik info** sectie.</span><span class="sxs-lookup"><span data-stu-id="4eb06-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="4eb06-139">Kopieer en sla de **primaire sleutel** en de **aanvragen en antwoorden** URL.</span><span class="sxs-lookup"><span data-stu-id="4eb06-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="4eb06-140">In Excel, gaat u naar de **webservices** sectie (als u zich in de **Predict** sectie, klikt u op de pijl naar links naar de lijst met web-services).</span><span class="sxs-lookup"><span data-stu-id="4eb06-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Ga naar de Web service selecteren][03]
5. <span data-ttu-id="4eb06-142">Klik op **-webservice toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="4eb06-143">Plak de URL in de Excel-invoegtoepassing tekstvak met het label **URL**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="4eb06-144">Plak de API/primaire sleutel in het tekstvak met het label **API-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="4eb06-145">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="4eb06-145">Click **Add**.</span></span>
   
    ![URL en API-sleutel voor een klassieke webservice.][06]
9. <span data-ttu-id="4eb06-147">Volg voor het gebruik van de webservice, de voorgaande instructies, 'Stappen voor het gebruik van een bestaande web Service'.</span><span class="sxs-lookup"><span data-stu-id="4eb06-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="4eb06-148">Delen van uw werkmap</span><span class="sxs-lookup"><span data-stu-id="4eb06-148">Sharing Your Workbook</span></span>
<span data-ttu-id="4eb06-149">Als u de werkmap opslaan, klikt u vervolgens de API/primaire sleutel voor de webservices die u hebt toegevoegd ook opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4eb06-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="4eb06-150">Dit betekent dat u moet de werkmap alleen delen met personen die u vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="4eb06-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="4eb06-151">Vragen te stellen in de volgende sectie Opmerking of op onze [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4eb06-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
