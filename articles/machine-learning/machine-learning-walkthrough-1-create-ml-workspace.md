---
title: 'Stap 1: Een Machine Learning-werkruimte maken | Microsoft Docs'
description: 'Stap 1 van Hallo een overzicht van de voorspellende oplossing ontwikkelen: meer informatie over hoe tooset een nieuwe Azure Machine Learning Studio-werkruimte.'
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
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a><span data-ttu-id="b4cdb-103">Kennismaken, stap 1: Een Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="b4cdb-103">Walkthrough Step 1: Create a Machine Learning workspace</span></span>
<span data-ttu-id="b4cdb-104">Dit is de eerste stap Hallo van Hallo-rondleiding [predictive analytics-oplossing in Azure Machine Learning ontwikkelen](machine-learning-walkthrough-develop-predictive-solution.md).</span><span class="sxs-lookup"><span data-stu-id="b4cdb-104">This is hello first step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).</span></span>

1. <span data-ttu-id="b4cdb-105">**Een Machine Learning-werkruimte maken**</span><span class="sxs-lookup"><span data-stu-id="b4cdb-105">**Create a Machine Learning workspace**</span></span>
2. [<span data-ttu-id="b4cdb-106">Bestaande gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="b4cdb-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="b4cdb-107">Een nieuw experiment maken</span><span class="sxs-lookup"><span data-stu-id="b4cdb-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="b4cdb-108">Trainen en evalueren Hallo modellen</span><span class="sxs-lookup"><span data-stu-id="b4cdb-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="b4cdb-109">Hallo-webservice implementeren</span><span class="sxs-lookup"><span data-stu-id="b4cdb-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="b4cdb-110">Toegang tot Hallo-webservice</span><span class="sxs-lookup"><span data-stu-id="b4cdb-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

<span data-ttu-id="b4cdb-111">toouse Machine Learning Studio, moet u toohave een Microsoft Azure Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-111">toouse Machine Learning Studio, you need toohave a Microsoft Azure Machine Learning workspace.</span></span> <span data-ttu-id="b4cdb-112">Deze werkruimte bevat Hallo hulpmiddelen die u nodig hebt toocreate, beheren en experimenten publiceren.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-112">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

<span data-ttu-id="b4cdb-113">Hallo beheerder voor uw Azure-abonnement toocreate Hallo werkruimte moet en voegt u vervolgens als een eigenaar of Bijdrager.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-113">hello administrator for your Azure subscription needs toocreate hello workspace and then add you as an owner or contributor.</span></span> <span data-ttu-id="b4cdb-114">Zie voor meer informatie [maken en delen van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="b4cdb-114">For details, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="b4cdb-115">Nadat uw werkruimte is gemaakt, opent u Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span><span class="sxs-lookup"><span data-stu-id="b4cdb-115">After your workspace is created, open Machine Learning Studio ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)).</span></span> <span data-ttu-id="b4cdb-116">Als u meer dan één werkruimte hebt, kunt u Hallo werkruimte in Hallo werkbalk Hallo rechterbovenhoek van Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-116">If you have more than one workspace, you can select hello workspace in hello toolbar in hello upper-right corner of hello window.</span></span>

![Selecteer de werkruimte in Studio][2]

> [!TIP]
> <span data-ttu-id="b4cdb-118">Als u een eigenaar van het Hallo-werkruimte zijn aangebracht, kunt u Hallo experimenten u werkt waarmee met andere gebruikers uitnodigen delen toohello werkruimte.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-118">If you were made an owner of hello workspace, you can share hello experiments you're working on by inviting others toohello workspace.</span></span> <span data-ttu-id="b4cdb-119">U kunt dit doen in Machine Learning Studio op Hallo **instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-119">You can do this in Machine Learning Studio on hello **SETTINGS** page.</span></span> <span data-ttu-id="b4cdb-120">U hoeft alleen maar Hallo Microsoft-account of organisatie-account voor elke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-120">You just need hello Microsoft account or organizational account for each user.</span></span>
> 
> <span data-ttu-id="b4cdb-121">Op Hallo **instellingen** pagina, klikt u op **gebruikers**, klikt u vervolgens op **meer gebruikers UITNODIGEN** onderaan Hallo Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="b4cdb-121">On hello **SETTINGS** page, click **USERS**, then click **INVITE MORE USERS** at hello bottom of hello window.</span></span>
> 
> 

- - -
<span data-ttu-id="b4cdb-122">**Volgende stap: [bestaande gegevens uploaden](machine-learning-walkthrough-2-upload-data.md)**</span><span class="sxs-lookup"><span data-stu-id="b4cdb-122">**Next: [Upload existing data](machine-learning-walkthrough-2-upload-data.md)**</span></span>

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
