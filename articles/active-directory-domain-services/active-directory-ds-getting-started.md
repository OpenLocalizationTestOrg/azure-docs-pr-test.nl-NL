---
title: 'Azure Active Directory Domain Services: Aan de slag | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="c9b4c-103">Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen</span><span class="sxs-lookup"><span data-stu-id="c9b4c-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="c9b4c-104">Dit artikel laat zien hoe tooenable Azure Active Directory Domain Services (Azure AD DS) met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="c9b4c-105">Hallo toolaunch **inschakelen Azure AD Domain Services** wizard, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c9b4c-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="c9b4c-106">Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9b4c-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c9b4c-107">Klik in het linkerdeelvenster Hallo op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="c9b4c-108">In Hallo **nieuw** blade, type **domeinservices** in Hallo zoekbalk.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Zoeken naar domeinservices](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="c9b4c-110">Klik op tooselect **Azure AD Domain Services** uit de lijst Hallo van zoeksuggesties.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="c9b4c-111">Op Hallo **Azure AD Domain Services** blade, klikt u op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Domain services-blade](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="c9b4c-113">Hallo **inschakelen Azure AD Domain Services** wizard wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="c9b4c-114">Taak 1: basisinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="c9b4c-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="c9b4c-115">In Hallo **basisbeginselen** pagina van wizard hello, kunt u Hallo DNS-domeinnaam voor het beheerde domein Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="c9b4c-116">U kunt ook Hallo resourcegroep en Azure-locatie toowhich Hallo beheerd domein moet worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Basisprincipes configureren](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="c9b4c-118">Kies Hallo **DNS-domeinnaam** voor uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="c9b4c-119">Hallo standaarddomeinnaam van Hallo-map (met een **. onmicrosoft.com** achtervoegsel) standaard is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="c9b4c-120">U kunt er ook voor typen in een aangepaste domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="c9b4c-121">In dit voorbeeld wordt de aangepaste domeinnaam Hallo is *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="c9b4c-122">Hallo-voorvoegsel van de opgegeven domeinnaam (bijvoorbeeld *contoso100* in Hallo *contoso100.com* domeinnaam) moet 15 of minder tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="c9b4c-123">U kunt een beheerd domein maken met een voorvoegsel langer is dan 15 tekens.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="c9b4c-124">Zorg ervoor dat die Hallo DNS-domeinnaam die u hebt gekozen voor Hallo beheerd domein nog niet bestaat in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="c9b4c-125">Controleer in het bijzonder of:</span><span class="sxs-lookup"><span data-stu-id="c9b4c-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="c9b4c-126">U hebt al een domein met Hallo dezelfde DNS-domeinnaam op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="c9b4c-127">Hallo virtueel netwerk waar u van plan tooenable Hallo beheerd domein bent heeft een VPN-verbinding met uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="c9b4c-128">In dit scenario, zorg ervoor dat u hebt geen een domein met Hallo dezelfde DNS-domeinnaam op uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="c9b4c-129">U hebt een bestaande cloudservice met die naam op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="c9b4c-130">Kies Hallo **type virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="c9b4c-131">Standaard Hallo **Resource Manager** type virtueel netwerk dat is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="c9b4c-132">Het wordt aangeraden om dit type virtueel netwerk gebruiken voor alle beheerde domeinen van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="c9b4c-133">Selecteer hello Azure **abonnement** waarin u wilt toocreate Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="c9b4c-134">Selecteer Hallo **resourcegroep** moet deel uitmaken van toowhich Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="c9b4c-135">U kunt beide Hallo **nieuw** of **gebruik bestaande** opties tooselect Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="c9b4c-136">Kies hello Azure **locatie** aan welke Hallo beheerd domein moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="c9b4c-137">Op Hallo **netwerk** pagina van wizard hello, ziet u alleen virtuele netwerken die deel uitmaken van toohello locatie die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="c9b4c-138">Wanneer u klaar bent, klikt u op **OK** toomove op toohello **netwerk** pagina van wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="c9b4c-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="c9b4c-139">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="c9b4c-139">Next step</span></span>
[<span data-ttu-id="c9b4c-140">Taak 2: De netwerkinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="c9b4c-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
