---
title: een Machine Learning-werkruimte aaaCreate | Microsoft Docs
description: Hoe toocreate een werkruimte voor Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a><span data-ttu-id="5471d-103">Een Azure Machine Learning-werkruimte maken en delen</span><span class="sxs-lookup"><span data-stu-id="5471d-103">Create and share an Azure Machine Learning workspace</span></span>
<span data-ttu-id="5471d-104">Dit menu koppelingen tootopics waarin wordt beschreven hoe tooset up Hallo verschillende gegevens wetenschappelijke omgevingen gebruikt door Hallo Cortana Analytics proces (CAP's).</span><span class="sxs-lookup"><span data-stu-id="5471d-104">This menu links tootopics that describe how tooset up hello various data science environments used by hello Cortana Analytics Process (CAPS).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

<span data-ttu-id="5471d-105">Azure Machine Learning Studio toouse, moet u toohave een Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5471d-105">toouse Azure Machine Learning Studio, you need toohave a Machine Learning workspace.</span></span> <span data-ttu-id="5471d-106">Deze werkruimte bevat Hallo hulpmiddelen die u nodig hebt toocreate, beheren en experimenten publiceren.</span><span class="sxs-lookup"><span data-stu-id="5471d-106">This workspace contains hello tools you need toocreate, manage, and publish experiments.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a><span data-ttu-id="5471d-107">toocreate een werkruimte</span><span class="sxs-lookup"><span data-stu-id="5471d-107">toocreate a workspace</span></span>
1. <span data-ttu-id="5471d-108">Meld u aan toohello [Azure-portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="5471d-108">Sign in toohello [Azure portal](https://portal.azure.com/)</span></span>

    > [!NOTE]
    > <span data-ttu-id="5471d-109">toosign in en een werkruimte maken, moet u toobe Azure-abonnementbeheerder.</span><span class="sxs-lookup"><span data-stu-id="5471d-109">toosign in and create a workspace, you need toobe an Azure subscription administrator.</span></span> 
    >
    > 

2. <span data-ttu-id="5471d-110">Klik op **+ nieuw**</span><span class="sxs-lookup"><span data-stu-id="5471d-110">Click **+New**</span></span>

3. <span data-ttu-id="5471d-111">Selecteer **Intelligence en analyse**, klikt u op **Machine Learning-werkruimte**, klikt u vervolgens op **maken**</span><span class="sxs-lookup"><span data-stu-id="5471d-111">Select **Intelligence + analytics**, click **Machine Learning Workspace**, then click **Create**</span></span>

4. <span data-ttu-id="5471d-112">Voer uw werkruimtegegevens</span><span class="sxs-lookup"><span data-stu-id="5471d-112">Enter your workspace information</span></span>

    - <span data-ttu-id="5471d-113">Hallo *Werkruimtenaam* mogelijk up too260 tekens, niet eindigen met een spatie.</span><span class="sxs-lookup"><span data-stu-id="5471d-113">hello *workspace name* may be up too260 characters, not ending in a space.</span></span> <span data-ttu-id="5471d-114">Hallo-naam kan niet deze tekens bevatten:`< > * % & : \ ? + /`</span><span class="sxs-lookup"><span data-stu-id="5471d-114">hello name can't include these characters: `< > * % & : \ ? + /`</span></span>
    - <span data-ttu-id="5471d-115">Hallo *web service-abonnement* u kiest (of maken), samen met de Hallo gekoppeld *prijscategorie* u selecteert, wordt gebruikt als u web-services uit deze werkruimte implementeert.</span><span class="sxs-lookup"><span data-stu-id="5471d-115">hello *web service plan* you choose (or create), along with hello associated *pricing tier* you select, is used if you deploy web services from this workspace.</span></span>

    ![Maak een nieuwe werkruimte](media/machine-learning-create-workspace/create-new-workspace.png)

5. <span data-ttu-id="5471d-117">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="5471d-117">Click **Create**</span></span>

<span data-ttu-id="5471d-118">Zodra Hallo werkruimte is geïmplementeerd, kunt u deze kunt openen in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5471d-118">Once hello workspace is deployed, you can open it in Machine Learning Studio.</span></span>

1. <span data-ttu-id="5471d-119">Blader tooMachine Learning Studio op [https://studio.azureml.net/](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5471d-119">Browse tooMachine Learning Studio at [https://studio.azureml.net/](https://studio.azureml.net/).</span></span>

2. <span data-ttu-id="5471d-120">Selecteer uw werkruimte in Hallo upper--rechterhoek.</span><span class="sxs-lookup"><span data-stu-id="5471d-120">Select your workspace in hello upper-right-hand corner.</span></span>

    ![Werkruimte selecteren](media/machine-learning-create-workspace/open-workspace.png)

3. <span data-ttu-id="5471d-122">Klik op **mijn experimenten**.</span><span class="sxs-lookup"><span data-stu-id="5471d-122">Click **my experiments**.</span></span>

    ![Open experimenten](media/machine-learning-create-workspace/my-experiments.png)

<span data-ttu-id="5471d-124">Zie voor meer informatie over het beheren van uw werkruimte [beheren van een Azure Machine Learning-werkruimte](machine-learning-manage-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="5471d-124">For information about managing your workspace, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
<span data-ttu-id="5471d-125">Als er een probleem bij het maken van uw werkruimte optreden, Raadpleeg [Troubleshooting guide: maken en koppelen van de Machine Learning-werkruimte tooa](machine-learning-troubleshooting-creating-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="5471d-125">If you encounter a problem creating your workspace, see [Troubleshooting guide: Create and connect tooa Machine Learning workspace](machine-learning-troubleshooting-creating-ml-workspace.md).</span></span>


## <a name="sharing-an-azure-machine-learning-workspace"></a><span data-ttu-id="5471d-126">Delen van een Azure Machine Learning-werkruimte</span><span class="sxs-lookup"><span data-stu-id="5471d-126">Sharing an Azure Machine Learning workspace</span></span>
<span data-ttu-id="5471d-127">Zodra een Machine Learning-werkruimte is gemaakt, kunt u uitnodigen gebruikers tooyour werkruimte tooshare toegang tooyour werkruimte en alle bijbehorende experimenten, gegevenssets, laptops, enzovoort. U kunt gebruikers toevoegen in een van twee functies:</span><span class="sxs-lookup"><span data-stu-id="5471d-127">Once a Machine Learning workspace is created, you can invite users tooyour workspace tooshare access tooyour workspace and all its experiments, datasets, notebooks, etc. You can add users in one of two roles:</span></span>

* <span data-ttu-id="5471d-128">**Gebruiker** -werkruimte van een gebruiker kunt maken, openen, wijzigen en experimenten, gegevenssets, enz. in de werkruimte Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5471d-128">**User** - A workspace user can create, open, modify, and delete experiments, datasets, etc. in hello workspace.</span></span>
* <span data-ttu-id="5471d-129">**Eigenaar** - eigenaar kunt uitnodigen en gebruikers in de werkruimte Hallo in toowhat toevoeging van een gebruiker verwijderen kunnen doen.</span><span class="sxs-lookup"><span data-stu-id="5471d-129">**Owner** - An owner can invite and remove users in hello workspace, in addition toowhat a user can do.</span></span>

> [!NOTE]
> <span data-ttu-id="5471d-130">Hallo administrator-account dat Hallo werkruimte maakt toohello werkruimte automatisch toegevoegd als eigenaar-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5471d-130">hello administrator account that creates hello workspace is automatically added toohello workspace as workspace Owner.</span></span> <span data-ttu-id="5471d-131">Echter andere beheerders of gebruikers in de betreffende abonnement zijn niet automatisch toegangsrechten toohello-werkruimte: u hebt tooinvite nodig ze expliciet.</span><span class="sxs-lookup"><span data-stu-id="5471d-131">However, other administrators or users in that subscription are not automatically granted access toohello workspace - you need tooinvite them explicitly.</span></span>
> 
> 

### <a name="tooshare-a-workspace"></a><span data-ttu-id="5471d-132">tooshare een werkruimte</span><span class="sxs-lookup"><span data-stu-id="5471d-132">tooshare a workspace</span></span>

1. <span data-ttu-id="5471d-133">Meld u aan tooMachine Learning Studio [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span><span class="sxs-lookup"><span data-stu-id="5471d-133">Sign in tooMachine Learning Studio at [https://studio.azureml.net/Home](https://studio.azureml.net/Home)</span></span>

2. <span data-ttu-id="5471d-134">Klik in het linkerdeelvenster Hallo **instellingen**</span><span class="sxs-lookup"><span data-stu-id="5471d-134">In hello left panel, click **SETTINGS**</span></span>

3. <span data-ttu-id="5471d-135">Klik op Hallo **gebruikers** tabblad</span><span class="sxs-lookup"><span data-stu-id="5471d-135">Click hello **USERS** tab</span></span>

4. <span data-ttu-id="5471d-136">Klik op **meer gebruikers UITNODIGEN** onderaan Hallo Hallo pagina</span><span class="sxs-lookup"><span data-stu-id="5471d-136">Click **INVITE MORE USERS** at hello bottom of hello page</span></span>

    ![Studio-instellingen](media/machine-learning-create-workspace/settings.png)

5. <span data-ttu-id="5471d-138">Voer een of meer e-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="5471d-138">Enter one or more email addresses.</span></span> <span data-ttu-id="5471d-139">Hallo-gebruikers moeten een geldig Microsoft-account of een organisatie-account (van Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5471d-139">hello users need a valid Microsoft account or an organizational account (from Azure Active Directory).</span></span>

6. <span data-ttu-id="5471d-140">Selecteer of u wilt dat tooadd Hallo gebruikers als eigenaar of gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5471d-140">Select whether you want tooadd hello users as Owner or User.</span></span>

7. <span data-ttu-id="5471d-141">Klik op Hallo **OK** vinkje knop.</span><span class="sxs-lookup"><span data-stu-id="5471d-141">Click hello **OK** checkmark button.</span></span>

<span data-ttu-id="5471d-142">Elke gebruiker die u toevoegt, ontvangt een e-mail met instructies over hoe toosign in toohello werkruimte gedeeld.</span><span class="sxs-lookup"><span data-stu-id="5471d-142">Each user you add will receive an email with instructions on how toosign in toohello shared workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="5471d-143">Voor gebruikers toobe kunnen toodeploy of webservices in deze werkruimte wilt beheren, moeten ze een bijdrager of een beheerder in hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5471d-143">For users toobe able toodeploy or manage web services in this workspace, they must be a contributor or administrator in hello Azure subscription.</span></span> 



