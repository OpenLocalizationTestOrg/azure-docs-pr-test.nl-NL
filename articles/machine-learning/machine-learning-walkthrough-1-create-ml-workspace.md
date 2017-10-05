---
title: 'Stap 1: Een Machine Learning-werkruimte maken | Microsoft Docs'
description: 'Stap 1 van het ontwikkelen van een overzicht van de voorspellende oplossing: informatie over het instellen van een nieuwe Azure Machine Learning Studio-werkruimte.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 8ca42ef8f5314866301f5c9e93caa90dc837a66e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="f50c5-103">Kennismaken, stap 1: Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="f50c5-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="f50c5-104">Dit is de eerste stap van de procedure [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="f50c5-104">This is the first step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="f50c5-105">**Een Machine Learning-werkruimte maken**</span><span class="sxs-lookup"><span data-stu-id="f50c5-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="f50c5-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="f50c5-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="f50c5-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="f50c5-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="f50c5-108">De modellen trainen en evalueren</span><span class="sxs-lookup"><span data-stu-id="f50c5-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="f50c5-109">De webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="f50c5-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="f50c5-110">Toegang tot de webservice</span><span class="sxs-lookup"><span data-stu-id="f50c5-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs to be updated to refer to the new way of creating workspaces in the Ibiza portal -->

<span data-ttu-id="f50c5-111">Voor het gebruik van Machine Learning Studio, moet u hebt een Microsoft Azure Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="f50c5-111">To use Machine Learning Studio, you need to have a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="f50c5-112">Deze werkruimte bevat de hulpprogramma's die u wilt maken, beheren en experimenten publiceren.</span><span class="sxs-lookup"><span data-stu-id="f50c5-112">This workspace contains the tools you need to create, manage, and publish experiments.</span></span>  

<!--
## To create a workspace
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com).
2. In the  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On the **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="f50c5-113">De beheerder voor uw Azure-abonnement moet maken van de werkruimte en u vervolgens toevoegen als een eigenaar of Bijdrager.</span><span class="sxs-lookup"><span data-stu-id="f50c5-113">The administrator for your Azure subscription needs to create the workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="f50c5-114">Zie voor meer informatie [maken en delen van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f50c5-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="f50c5-115">Nadat uw werkruimte is gemaakt, opent u Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="f50c5-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="f50c5-116">Als u meer dan één werkruimte hebt, kunt u de werkruimte op de werkbalk in de rechterbovenhoek van het venster.</span><span class="sxs-lookup"><span data-stu-id="f50c5-116">If you have more than one workspace, you can select the workspace in the toolbar in the upper-right corner of the window.</span></span>

![Selecteer de werkruimte in Studio][2]

> [!TIP]
> <span data-ttu-id="f50c5-118">Als u een eigenaar van de werkruimte zijn aangebracht, kunt u de u werkt waarmee met andere gebruikers in de werkruimte uitnodigen experimenten delen.</span><span class="sxs-lookup"><span data-stu-id="f50c5-118">If you were made an owner of the workspace, you can share the experiments you're working on by inviting others to the workspace.</span></span> <span data-ttu-id="f50c5-119">U kunt dit doen in Machine Learning Studio op de **instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="f50c5-119">You can do this in Machine Learning Studio on the **SETTINGS** page.</span></span> <span data-ttu-id="f50c5-120">U hoeft alleen maar de Microsoft-account of organisatie-account voor elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f50c5-120">You just need the Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="f50c5-121">Op de **instellingen** pagina, klikt u op **gebruikers**, klikt u vervolgens op **meer gebruikers UITNODIGEN** aan de onderkant van het venster.</span><span class="sxs-lookup"><span data-stu-id="f50c5-121">On the **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at the bottom of the window.</span></span>
> 
> 

- - -
<span data-ttu-id="f50c5-122">**Volgende stap: [bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="f50c5-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
