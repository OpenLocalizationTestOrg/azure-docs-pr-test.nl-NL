---
title: 'Azure Active Directory Domain Services: DC-beheerdersgroep hello Azure AD maken | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen
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
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="48453-103">Azure Active Directory Domain Services met behulp van de klassieke Azure-portal Hallo inschakelen</span><span class="sxs-lookup"><span data-stu-id="48453-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="48453-104">In dit artikel wordt beschreven en wordt begeleid Hallo configuratietaken die vereist voor u tooenable Azure Active Directory Domain Services (Azure AD DS) voor uw tenant van Azure Active Directory (Azure AD zijn).</span><span class="sxs-lookup"><span data-stu-id="48453-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="48453-105">[**Probeer in plaats daarvan het Hallo nieuwe (preview) Azure portal ervaring**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="48453-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="48453-106">Taak 1: Maak hello Azure AD DC-beheerdersgroep</span><span class="sxs-lookup"><span data-stu-id="48453-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="48453-107">de eerste taak Hallo is toocreate een beheergroep in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="48453-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="48453-108">Deze speciale beheerdersgroep heet *AAD DC beheerders*.</span><span class="sxs-lookup"><span data-stu-id="48453-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="48453-109">Leden van deze groep worden beheerdersmachtigingen op de computers die lid zijn van een domein toohello Azure Active Directory Domain Services beheerd domein zijn verleend.</span><span class="sxs-lookup"><span data-stu-id="48453-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="48453-110">Deze groep wordt de groep administrators toohello toegevoegd op domein machines.</span><span class="sxs-lookup"><span data-stu-id="48453-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="48453-111">Leden van deze groep kunnen ook op afstand toodomain die lid zijn van computers met extern bureaublad tooconnect gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48453-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="48453-112">U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op Hallo beheerde domein dat u hebt gemaakt met behulp van Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="48453-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="48453-113">Op de beheerde domeinen deze machtigingen zijn gereserveerd door het Hallo-service en zijn niet beschikbaar toousers binnen Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="48453-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="48453-114">U kunt echter gebruiken Hallo speciale beheergroep gemaakt in deze configuratie taak tooperform bevoegde enkele bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="48453-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="48453-115">Deze bewerkingen behoren lid te worden computers toohello domein, die deel uitmaken van de beheergroep toohello op machines domein en het configureren van Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="48453-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="48453-116">In deze configuratietaak Hallo beheergroep maken en toevoegen van een of meer gebruikers in uw directory toohello-groep.</span><span class="sxs-lookup"><span data-stu-id="48453-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="48453-117">toocreate Hallo-beheergroep van Azure Active Directory Domain Services, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="48453-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="48453-118">Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="48453-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="48453-119">Selecteer in het linkerdeelvenster Hallo Hallo **Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="48453-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="48453-120">Hello Azure AD-tenant (directory) dat waarvoor u tooenable Azure Active Directory Domain Services wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="48453-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="48453-121">U kunt slechts één domein voor elke Azure AD-directory maken.</span><span class="sxs-lookup"><span data-stu-id="48453-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="48453-123">Op Hallo **preview directory** pagina, klikt u op Hallo **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="48453-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="48453-124">Klik op tooadd een groep tooyour Azure AD-tenant, in het taakvenster Hallo HALLO hallo venster onderaan in **groep toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="48453-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![knop Hallo-groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="48453-126">In Hallo **groep toevoegen** dialoogvenster vak, maakt u een groep met de naam **AAD DC beheerders**, en stel vervolgens **groepstype** te**beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="48453-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="48453-127">tooenable toegang in uw Azure Active Directory Domain Services beheerd domein, een groep maken met deze naam.</span><span class="sxs-lookup"><span data-stu-id="48453-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![dialoogvenster Hallo-groep toevoegen](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="48453-129">In Hallo **beschrijving** vak, voer een beschrijving in waarmee anderen toounderstand deze codegroep beheerdersmachtigingen binnen Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="48453-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="48453-130">Nadat u Hallo groep hebt gemaakt, klikt u de eigenschappen op Hallo groep naam tooview.</span><span class="sxs-lookup"><span data-stu-id="48453-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="48453-131">tooadd gebruikers als leden van de groep hello, onderaan Hallo Hallo-venster, klikt u op Hallo **leden toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="48453-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Knop voor leden van groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="48453-133">In Hallo **leden toevoegen** in het dialoogvenster selecteert Hallo-gebruikers die moeten worden leden van deze groep en klik vervolgens op het vinkje Hallo op Hallo rechtsonder.</span><span class="sxs-lookup"><span data-stu-id="48453-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Tooadministrators gebruikersgroep toevoegen](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="48453-135">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="48453-135">Next step</span></span>
[<span data-ttu-id="48453-136">Taak 2: Maak of Selecteer een Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="48453-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
