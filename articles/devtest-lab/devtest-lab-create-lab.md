---
title: Een lab maken in Azure DevTest Labs | Microsoft Docs
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
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="3f284-103">Een lab maken in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3f284-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="3f284-104">Een lab in Azure DevTest Labs is de infrastructuur die een groep resources omvat, zoals VM's (virtuele machines), waarmee u deze resources beter kunt beheren door limieten en quota op te geven.</span><span class="sxs-lookup"><span data-stu-id="3f284-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="3f284-105">In dit artikel wordt uitgelegd hoe u een lab maakt met behulp van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3f284-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f284-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f284-106">Prerequisites</span></span>
<span data-ttu-id="3f284-107">Als u een lab wilt maken, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="3f284-107">To create a lab, you need:</span></span>

* <span data-ttu-id="3f284-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f284-108">An Azure subscription.</span></span> <span data-ttu-id="3f284-109">Zie [Azure aanschaffen](https://azure.microsoft.com/pricing/purchase-options/) of [Gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie over Azure-aankoopopties.</span><span class="sxs-lookup"><span data-stu-id="3f284-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="3f284-110">U moet de eigenaar van het abonnement zijn om het lab te maken.</span><span class="sxs-lookup"><span data-stu-id="3f284-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="3f284-111">Stappen voor het maken van een lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3f284-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="3f284-112">In de volgende stappen ziet u hoe u Azure Portal kunt gebruiken om een lab te maken in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="3f284-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="3f284-113">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3f284-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="3f284-114">Selecteer in het hoofdmenu aan de linkerkant **Meer services** (onder aan de lijst).</span><span class="sxs-lookup"><span data-stu-id="3f284-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![Menuoptie Meer services](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="3f284-116">Selecteer **DevTest Labs** in de lijst met beschikbare services.</span><span class="sxs-lookup"><span data-stu-id="3f284-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="3f284-117">Selecteer op de blade **DevTest Labs** de optie **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3f284-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Een lab toevoegen](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="3f284-119">Op de blade **Een DevTest Lab maken**:</span><span class="sxs-lookup"><span data-stu-id="3f284-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="3f284-120">Voer een **labnaam** in voor het nieuwe lab.</span><span class="sxs-lookup"><span data-stu-id="3f284-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="3f284-121">Selecteer het **abonnement** dat u wilt koppelen aan het lab.</span><span class="sxs-lookup"><span data-stu-id="3f284-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="3f284-122">Selecteer op welke **locatie** u het lab wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="3f284-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="3f284-123">Selecteer **Auto-shutdown** om op te geven of u het automatisch afsluiten van alle virtuele machines van het lab wilt inschakelen en de parameters voor deze machines wilt definiëren.</span><span class="sxs-lookup"><span data-stu-id="3f284-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="3f284-124">De functie Auto-shutdown is voornamelijk een kostenbesparende functie waar u kunt opgeven wanneer de VM automatisch moet worden afgesloten.</span><span class="sxs-lookup"><span data-stu-id="3f284-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="3f284-125">Nadat u een lab hebt gemaakt, kunt u de Auto-shutdown-instellingen wijzigen door de stappen te volgen in het artikel [Alle beleidsregels beheren voor een lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="3f284-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="3f284-126">Selecteer **Vastmaken aan dashboard** als u wilt dat een snelkoppeling van de testomgeving op het dashboard van de portal wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f284-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="3f284-127">Selecteer **Opties voor Automation** als u Azure Resource Manager-sjablonen wilt ophalen voor automatisering van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="3f284-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="3f284-128">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="3f284-128">Select **Create**.</span></span> <span data-ttu-id="3f284-129">Nadat u **Maken** hebt geselecteerd, wordt de blade **DevTest Labs** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3f284-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="3f284-130">U kunt de vorderingen bij het maken van het lab bijhouden in de sectie **Meldingen**.</span><span class="sxs-lookup"><span data-stu-id="3f284-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="3f284-131">Zodra het maken is voltooid, vernieuwt u de pagina en ziet u het zojuist gemaakte lab in de lijst met labs.</span><span class="sxs-lookup"><span data-stu-id="3f284-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![Een labblade maken](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="3f284-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f284-133">Next steps</span></span>
<span data-ttu-id="3f284-134">Wanneer u uw lab hebt gemaakt, kunt u onder andere de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3f284-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="3f284-135">[Toegang tot een lab beveiligen](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="3f284-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="3f284-136">[Labbeleidsregels instellen](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3f284-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="3f284-137">[Een labsjabloon maken](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="3f284-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="3f284-138">[Aangepaste artefacten maken voor uw virtuele machines](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="3f284-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="3f284-139">[Een VM met artefacten toevoegen aan een lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="3f284-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

