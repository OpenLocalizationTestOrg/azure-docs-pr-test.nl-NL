---
title: aaaCreate een lab in Azure DevTest Labs | Microsoft Docs
description: Een lab voor virtuele machines maken in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bc6b4-103">Een lab maken in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bc6b4-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="bc6b4-104">Een lab in Azure DevTest Labs is Hallo-infrastructuur die een groep resources omvat, zoals virtuele Machines (VM's), waarmee u betere die bronnen beheren door te geven limieten en quota's.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="bc6b4-105">In dit artikel begeleidt u bij Hallo-proces voor het maken van een testomgeving met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc6b4-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bc6b4-106">Prerequisites</span></span>
<span data-ttu-id="bc6b4-107">een lab toocreate, moet u de:</span><span class="sxs-lookup"><span data-stu-id="bc6b4-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="bc6b4-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-108">An Azure subscription.</span></span> <span data-ttu-id="bc6b4-109">Zie toolearn over Azure-Aankoopopties [hoe toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) of [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="bc6b4-110">U moet eigenaar van de Hallo Hallo abonnement toocreate Hallo Lab.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bc6b4-111">Stappen toocreate een lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bc6b4-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="bc6b4-112">Hallo stappen laten zien hoe toouse hello Azure portal toocreate een lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="bc6b4-113">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="bc6b4-114">Selecteer in het hoofdmenu Hallo aan de linkerkant Hallo **meer Services** (onderaan Hallo Hallo lijst).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Menuoptie Meer services](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="bc6b4-116">Uit de lijst met beschikbare services Hallo **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="bc6b4-117">Op Hallo **DevTest Labs** blade Selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Een lab toevoegen](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="bc6b4-119">Op Hallo **een DevTest Lab maken** blade:</span><span class="sxs-lookup"><span data-stu-id="bc6b4-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="bc6b4-120">Voer een **Labnaam** voor Hallo nieuwe lab.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="bc6b4-121">Selecteer Hallo **abonnement** tooassociate met Hallo lab.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="bc6b4-122">Selecteer een **locatie** in welke toostore Hallo-testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="bc6b4-123">Selecteer **automatisch afsluiten** toospecify als u wilt dat tooenable - en Hallo parameters definiëren voor - Hallo automatisch afsluiten van alle Hallo lab van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="bc6b4-124">Hallo automatisch afsluiten functie is vooral een kostenbesparende waarbij u kunt opgeven wanneer het gewenste VM Hallo tooautomatically worden afgesloten.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="bc6b4-125">U kunt instellingen voor automatisch afsluiten wijzigen na het maken van Hallo lab Hallo stappen die worden beschreven in artikel Hallo [beheren van alle beleidsregels voor een testomgeving in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="bc6b4-126">Selecteer **pincode tooDashboard** als u wilt dat een snelkoppeling van Hallo lab tooappear op Hallo-portaldashboard.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="bc6b4-127">Selecteer **automatiseringsopties** tooget Azure Resource Manager-sjablonen voor het automatiseren van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="bc6b4-128">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-128">Select **Create**.</span></span> <span data-ttu-id="bc6b4-129">Na het selecteren van **maken**, Hallo **DevTest Labs** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="bc6b4-130">U kunt de status Hallo van proces voor het maken van lab Hallo bewaken door bekijkt hello **meldingen** gebied.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="bc6b4-131">Als voltooid, vernieuwen Hallo pagina toosee Hallo nieuw lab gemaakt in de lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="bc6b4-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Een labblade maken](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bc6b4-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc6b4-133">Next steps</span></span>
<span data-ttu-id="bc6b4-134">Als u uw lab hebt gemaakt, vindt hier u enkele tooconsider met volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="bc6b4-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="bc6b4-135">[Veilige toegang tooa lab](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="bc6b4-136">[Labbeleidsregels instellen](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="bc6b4-137">[Een labsjabloon maken](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="bc6b4-138">[Aangepaste artefacten maken voor uw virtuele machines](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="bc6b4-139">[Toevoegen van een VM met artefacten tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="bc6b4-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

