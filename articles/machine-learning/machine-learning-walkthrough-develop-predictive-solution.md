---
title: aaaA voorspellende oplossing voor kredietrisico met Machine Learning | Microsoft Docs
description: Een gedetailleerde procedure hoe toocreate predictive analytics-oplossing voor tegoed risicoanalyse in Azure Machine Learning Studio.
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
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="40843-104">Procedure: een predictive analytics-oplossing opzetten voor kredietrisicobeoordeling in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40843-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="40843-105">In dit overzicht nemen we een uitgebreide blik op Hallo-proces voor het ontwikkelen van een predictive analytics-oplossing in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="40843-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="40843-106">We een eenvoudige model in Machine Learning Studio ontwikkelen en vervolgens te implementeren als een Azure Machine Learning-webservice waar Hallo model voorspellingen met nieuwe gegevens kunt maken.</span><span class="sxs-lookup"><span data-stu-id="40843-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="40843-107">In deze rondleiding gaan we ervan uit dat u Machine Learning Studio al minstens één keer hebt gebruikt en dat u enig inzicht hebt in de concepten van machine learning.</span><span class="sxs-lookup"><span data-stu-id="40843-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="40843-108">Er wordt niet van uitgegaan dat u een expert bent.</span><span class="sxs-lookup"><span data-stu-id="40843-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="40843-109">Als u nog nooit hebt gebruikt **Azure Machine Learning Studio** voordat toostart met Hallo zelfstudie, kunt u [maken uw eerste gegevenswetenschap experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="40843-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="40843-110">Deze zelfstudie leert u Machine Learning Studio voor Hallo eerst.</span><span class="sxs-lookup"><span data-stu-id="40843-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="40843-111">Hier ziet u Hallo basisprincipes van hoe toodrag-en-neerzetten modules naar uw experiment ze met elkaar verbinden, Hallo experiment uitvoeren en bekijkt hello resultaten.</span><span class="sxs-lookup"><span data-stu-id="40843-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="40843-112">Een ander hulpprogramma die mogelijk nuttig voor het aan de slag is een diagram waarin u een van Hallo-mogelijkheden van Machine Learning Studio overzicht.</span><span class="sxs-lookup"><span data-stu-id="40843-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="40843-113">U kunt dit hier downloaden en afdrukken: [Overzichtsdiagram van de mogelijkheden van Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).</span><span class="sxs-lookup"><span data-stu-id="40843-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="40843-114">Als u nieuwe toohello veld van machine learning in het algemeen, moet u er een video series die mogelijk nuttig tooyou is.</span><span class="sxs-lookup"><span data-stu-id="40843-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="40843-115">Wordt aangeroepen [Gegevenswetenschap voor beginnende gebruikers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) en deze krijgt u een goede inleiding toomachine learning met alledaagse taal en -concepten.</span><span class="sxs-lookup"><span data-stu-id="40843-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="40843-116">Hallo probleem</span><span class="sxs-lookup"><span data-stu-id="40843-116">hello problem</span></span>

<span data-ttu-id="40843-117">Stel dat u iemands kredietrisico op basis van Hallo informatie die ze in een kredietaanvraag heeft toopredict nodig.</span><span class="sxs-lookup"><span data-stu-id="40843-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="40843-118">Kredietrisicobeoordeling is een complex probleem, maar in het kader van deze rondleiding stellen we de zaken wat eenvoudiger voor.</span><span class="sxs-lookup"><span data-stu-id="40843-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="40843-119">We nemen kredietrisicobeoordeling als voorbeeld van hoe u een predictive analytics-oplossing kunt maken met behulp van Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="40843-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="40843-120">toodo, gebruiken we Azure Machine Learning Studio en een Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="40843-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="40843-121">Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="40843-121">hello solution</span></span>

<span data-ttu-id="40843-122">In deze gedetailleerde rondleiding beginnen we met openbaar beschikbare kredietrisicogegevens, en ontwikkelen en trainen we op basis van die gegevens een voorspellend model.</span><span class="sxs-lookup"><span data-stu-id="40843-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="40843-123">Vervolgens we Hallo model implementeren als een webservice zodat deze kan worden gebruikt door anderen voor kredietrisicobeoordeling.</span><span class="sxs-lookup"><span data-stu-id="40843-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="40843-124">toocreate deze oplossing voor kredietrisicobeoordeling, er als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="40843-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="40843-125">Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="40843-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="40843-126">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="40843-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="40843-127">Een experiment maken</span><span class="sxs-lookup"><span data-stu-id="40843-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="40843-128">Trainen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="40843-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="40843-129">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="40843-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="40843-130">Toegang Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="40843-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="40843-131">U vindt een werkexemplaar van Hallo experiment die we ontwikkelen in dit scenario in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="40843-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="40843-132">Ga te**[scenario - tegoed risico voorspelling](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  en klik op **openen in Studio** toodownload een kopie van het Hallo-experiment in uw werkruimte van Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="40843-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="40843-133">In dit scenario is gebaseerd op een vereenvoudigde versie van het voorbeeldexperiment hello, [binaire classificatie: Credit risico voorspelling](http://go.microsoft.com/fwlink/?LinkID=525270), ook beschikbaar in Hallo [galerie](http://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="40843-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
