---
title: Een voorspelde oplossing voor kredietrisico met Machine Learning | Microsoft Docs
description: Een gedetailleerde procedure voor het maken van een predictive analytics-oplossing voor kredietrisicobeoordeling in Azure Machine Learning Studio.
keywords: kredietrisico, predictive analytics-oplossing, risico-evaluatie
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="69828-104">Procedure: een predictive analytics-oplossing opzetten voor kredietrisicobeoordeling in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="69828-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="69828-105">In deze rondleiding gaan we uitgebreid in op het ontwikkelingsproces van een predictive analytics-oplossing in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="69828-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="69828-106">We zetten een eenvoudig model op in Machine Learning Studio en implementeren dit vervolgens als Azure Machine Learning-webservice, zodat het model voorspellingen kan doen met nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="69828-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="69828-107">In deze rondleiding gaan we ervan uit dat u Machine Learning Studio al minstens één keer hebt gebruikt en dat u enig inzicht hebt in de concepten van machine learning.</span><span class="sxs-lookup"><span data-stu-id="69828-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="69828-108">Er wordt niet van uitgegaan dat u een expert bent.</span><span class="sxs-lookup"><span data-stu-id="69828-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="69828-109">Als u **Azure Machine Learning Studio** nog nooit eerder hebt gebruikt, doet u er verstandig aan te beginnen met de zelfstudie [Uw eerste gegevenswetenschapexperiment maken in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="69828-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="69828-110">In die zelfstudie doorloopt u Machine Learning Studio voor de eerste keer.</span><span class="sxs-lookup"><span data-stu-id="69828-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="69828-111">U ziet hoe u modules naar uw experiment sleept, ze aan elkaar koppelt, het experiment uitvoert en de resultaten weergeeft.</span><span class="sxs-lookup"><span data-stu-id="69828-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="69828-112">Een ander hulpmiddel dat handig kan zijn wanneer u aan de slag gaat, is een diagram met een overzicht van de mogelijkheden van Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="69828-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="69828-113">U kunt dit hier downloaden en afdrukken: [Overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="69828-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="69828-114">Als u geen ervaring hebt met machine learning in het algemeen, bekijk dan eerst onze informatieve videoserie.</span><span class="sxs-lookup"><span data-stu-id="69828-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="69828-115">Deze heet [Wetenschappelijke gegevens voor beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) en geeft u met alledaagse taal en concepten een uitgebreide inleiding tot machine learning.</span><span class="sxs-lookup"><span data-stu-id="69828-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="69828-116">Het probleem</span><span class="sxs-lookup"><span data-stu-id="69828-116">The problem</span></span>

<span data-ttu-id="69828-117">Stel dat u iemands kredietrisico moet voorspellen op basis van de gegevens die deze persoon in een kredietaanvraag heeft ingevuld.</span><span class="sxs-lookup"><span data-stu-id="69828-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="69828-118">Kredietrisicobeoordeling is een complex probleem, maar in het kader van deze rondleiding stellen we de zaken wat eenvoudiger voor.</span><span class="sxs-lookup"><span data-stu-id="69828-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="69828-119">We nemen kredietrisicobeoordeling als voorbeeld van hoe u een predictive analytics-oplossing kunt maken met behulp van Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="69828-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="69828-120">Hiervoor gebruiken we Azure Machine Learning Studio en een Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="69828-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="69828-121">De oplossing</span><span class="sxs-lookup"><span data-stu-id="69828-121">The solution</span></span>

<span data-ttu-id="69828-122">In deze gedetailleerde rondleiding beginnen we met openbaar beschikbare kredietrisicogegevens, en ontwikkelen en trainen we op basis van die gegevens een voorspellend model.</span><span class="sxs-lookup"><span data-stu-id="69828-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="69828-123">Vervolgens implementeren we het model als webservice, zodat het door anderen kan worden gebruikt voor kredietrisicobeoordeling.</span><span class="sxs-lookup"><span data-stu-id="69828-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="69828-124">Voer de volgende stappen uit als u deze oplossing voor kredietrisicobeoordeling wilt maken:</span><span class="sxs-lookup"><span data-stu-id="69828-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="69828-125">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="69828-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="69828-126">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="69828-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="69828-127">Een experiment maken</span><span class="sxs-lookup"><span data-stu-id="69828-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="69828-128">De modellen trainen en evalueren</span><span class="sxs-lookup"><span data-stu-id="69828-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="69828-129">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="69828-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="69828-130">De webservice openen</span><span class="sxs-lookup"><span data-stu-id="69828-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="69828-131">Een werkende kopie van het experiment dat we in deze rondleiding ontwikkelen, vindt u in de [Cortana Intelligence-galerie](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="69828-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="69828-132">Ga naar **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** en klik op **Open in Studio** om een kopie van het experiment naar uw Machine Learning Studio-werkruimte te downloaden.</span><span class="sxs-lookup"><span data-stu-id="69828-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="69828-133">Deze rondleiding is gebaseerd op een vereenvoudigde versie van het voorbeeldexperiment [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), dat eveneens beschikbaar is in de [galerij](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="69828-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
