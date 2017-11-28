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
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="2c578-103">Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen</span><span class="sxs-lookup"><span data-stu-id="2c578-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="2c578-104">Taak 3: beheergroep configureren</span><span class="sxs-lookup"><span data-stu-id="2c578-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="2c578-105">In deze taak voor de configuratie maakt u een beheergroep in uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2c578-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="2c578-106">Deze speciale beheerdersgroep heet *AAD DC beheerders*.</span><span class="sxs-lookup"><span data-stu-id="2c578-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="2c578-107">Leden van deze groep worden beheerdersmachtigingen op de computers die lid zijn van een domein toohello beheerd domein zijn verleend.</span><span class="sxs-lookup"><span data-stu-id="2c578-107">Members of this group are granted administrative permissions on machines that are domain-joined toohello managed domain.</span></span> <span data-ttu-id="2c578-108">Deze groep wordt de groep administrators toohello toegevoegd op domein machines.</span><span class="sxs-lookup"><span data-stu-id="2c578-108">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="2c578-109">Leden van deze groep kunnen ook op afstand toodomain die lid zijn van computers met extern bureaublad tooconnect gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2c578-109">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="2c578-110">U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op Hallo beheerde domein dat u hebt gemaakt met behulp van Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="2c578-110">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="2c578-111">Op de beheerde domeinen deze machtigingen zijn gereserveerd door het Hallo-service en zijn niet beschikbaar toousers binnen Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="2c578-111">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="2c578-112">U kunt echter gebruiken Hallo speciale beheergroep gemaakt in deze configuratie taak tooperform bevoegde enkele bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2c578-112">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="2c578-113">Deze bewerkingen behoren lid te worden computers toohello domein, die deel uitmaken van de beheergroep toohello op machines domein en het configureren van Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="2c578-113">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="2c578-114">Hallo-beheergroep maakt Hallo wizard automatisch in uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="2c578-114">hello wizard automatically creates hello administrative group in your Azure AD directory.</span></span> <span data-ttu-id="2c578-115">Deze groep wordt 'AAD DC-beheerders' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2c578-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="2c578-116">Als u een bestaande groep met deze naam in uw Azure AD-directory hebt, geselecteerd Hallo wizard deze groep.</span><span class="sxs-lookup"><span data-stu-id="2c578-116">If you have an existing group with this name in your Azure AD directory, hello wizard selects this group.</span></span> <span data-ttu-id="2c578-117">U kunt configureren met behulp van Hallo groepslidmaatschap **beheerdersgroep** wizardpagina.</span><span class="sxs-lookup"><span data-stu-id="2c578-117">You can configure group membership using hello **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="2c578-118">groepslidmaatschap tooconfigure, klikt u op **AAD DC beheerders**.</span><span class="sxs-lookup"><span data-stu-id="2c578-118">tooconfigure group membership, click **AAD DC Administrators**.</span></span>

    ![Groepslidmaatschap configureren](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="2c578-120">Klik op Hallo **leden toevoegen** knop tooadd gebruikers van uw Azure AD directory toohello administrator-groep.</span><span class="sxs-lookup"><span data-stu-id="2c578-120">Click hello **Add members** button tooadd users from your Azure AD directory toohello administrator group.</span></span>

3. <span data-ttu-id="2c578-121">Wanneer u klaar bent, klikt u op **OK** toomove op toohello **samenvatting** pagina van wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="2c578-121">When you are done, click **OK** toomove on toohello **Summary** page of hello wizard.</span></span>

4. <span data-ttu-id="2c578-122">Op Hallo **samenvatting** pagina van wizard Hallo, bekijk Hallo configuratie-instellingen voor Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="2c578-122">On hello **Summary** page of hello wizard, review hello configuration settings for hello managed domain.</span></span> <span data-ttu-id="2c578-123">U kunt teruggaan tooany stap Hallo wizard toomake wijzigingen indien nodig.</span><span class="sxs-lookup"><span data-stu-id="2c578-123">You can go back tooany step of hello wizard toomake changes, if necessary.</span></span> <span data-ttu-id="2c578-124">Wanneer u klaar bent, klikt u op **OK** toocreate Hallo nieuw beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="2c578-124">When you are done, click **OK** toocreate hello new managed domain.</span></span>

    ![Samenvatting](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="2c578-126">U ziet een melding dat de voortgang Hallo van uw Azure AD Domain Services-implementatie geeft.</span><span class="sxs-lookup"><span data-stu-id="2c578-126">You see a notification that shows hello progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="2c578-127">Klik op Hallo melding toosee gedetailleerde uitgevoerd voor Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="2c578-127">Click hello notification toosee detailed progress for hello deployment.</span></span>

    ![Melding - implementatie wordt uitgevoerd](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="2c578-129">Inrichten van uw beheerde domein</span><span class="sxs-lookup"><span data-stu-id="2c578-129">Provision your managed domain</span></span>
<span data-ttu-id="2c578-130">Hallo-proces voor het leveren van uw beheerde domein kan tooan uur duren.</span><span class="sxs-lookup"><span data-stu-id="2c578-130">hello process of provisioning your managed domain can take up tooan hour.</span></span>

1. <span data-ttu-id="2c578-131">Tijdens de implementatie uitgevoerd wordt, kunt u zoeken naar domain services in Hallo **zoeken bronnen** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="2c578-131">While your deployment is in progress, you can search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="2c578-132">Selecteer **Azure AD Domain Services** van Hallo zoekresultaat.</span><span class="sxs-lookup"><span data-stu-id="2c578-132">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="2c578-133">Hallo **Azure AD Domain Services** blade bevat Hallo beheerde domein dat wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="2c578-133">hello **Azure AD Domain Services** blade lists hello managed domain that is being provisioned.</span></span>

    ![Zoeken naar beheerde domein wordt ingericht](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="2c578-135">Klik op Hallo-naam van Hallo beheerd domein (bijvoorbeeld, contoso100.com') toosee meer informatie over het Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="2c578-135">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services - status voor inrichten heeft](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="2c578-137">Hallo **overzicht** tabblad ziet u dat domein Hallo momenteel wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="2c578-137">hello **Overview** tab shows that hello domain is currently being provisioned.</span></span> <span data-ttu-id="2c578-138">U kunt Hallo beheerd domein niet configureren, totdat deze volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="2c578-138">You cannot configure hello managed domain until it is fully provisioned.</span></span> <span data-ttu-id="2c578-139">Het kan uw beheerde domein toobe volledig is ingericht tooan uur duren.</span><span class="sxs-lookup"><span data-stu-id="2c578-139">It may take up tooan hour for your managed domain toobe fully provisioned.</span></span>

    ![<span data-ttu-id="2c578-140">Domain Services - tabblad Overzicht tijdens Hallo Inrichtingsstatus</span><span class="sxs-lookup"><span data-stu-id="2c578-140">Domain Services - Overview tab during hello provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="2c578-141">Wanneer het beheerde domein Hallo volledig is ingericht, Hallo **overzicht** tabblad ziet u Hallo domein status als **met**.</span><span class="sxs-lookup"><span data-stu-id="2c578-141">When hello managed domain is fully provisioned, hello **Overview** tab shows hello domain status as **Running**.</span></span>

    ![Domain Services: tabblad Overzicht nadat het domein volledig is ingericht](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="2c578-143">Op Hallo **eigenschappen** tabblad ziet u twee IP-adressen op welk domein domeincontrollers beschikbaar voor Hallo virtueel netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="2c578-143">On hello **Properties** tab, you see two IP addresses at which domain controllers are available for hello virtual network.</span></span>

    ![Domain Services - tabblad Eigenschappen nadat het volledig is ingericht](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="2c578-145">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="2c578-145">Next step</span></span>
[<span data-ttu-id="2c578-146">Taak 4: Hallo DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="2c578-146">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
