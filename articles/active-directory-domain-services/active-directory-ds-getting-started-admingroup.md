---
title: 'Azure Active Directory Domain Services: Aan de slag | Microsoft Docs'
description: Azure Active Directory Domain Services met Azure portal (Preview) inschakelen
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
ms.openlocfilehash: f87bcf33d3b1eb21c7d84814e4c4086f664e293d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="523d9-103">Azure Active Directory Domain Services met Azure portal (Preview) inschakelen</span><span class="sxs-lookup"><span data-stu-id="523d9-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="task-3-configure-administrative-group"></a><span data-ttu-id="523d9-104">Taak 3: beheergroep configureren</span><span class="sxs-lookup"><span data-stu-id="523d9-104">Task 3: configure administrative group</span></span>
<span data-ttu-id="523d9-105">In deze taak voor de configuratie maakt u een beheergroep in uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="523d9-105">In this configuration task, you create an administrative group in your Azure AD directory.</span></span> <span data-ttu-id="523d9-106">Deze speciale beheerdersgroep heet *AAD DC beheerders*.</span><span class="sxs-lookup"><span data-stu-id="523d9-106">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="523d9-107">Leden van deze groep worden verleend beheerdersmachtigingen op de computers die zijn met het domein zijn toegevoegd aan het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="523d9-107">Members of this group are granted administrative permissions on machines that are domain-joined to the managed domain.</span></span> <span data-ttu-id="523d9-108">Op de machines domein, wordt deze groep toegevoegd aan de groep administrators.</span><span class="sxs-lookup"><span data-stu-id="523d9-108">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="523d9-109">Leden van deze groep kunnen ook extern bureaublad gebruiken extern verbinding maken met domein-machines.</span><span class="sxs-lookup"><span data-stu-id="523d9-109">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>

> [!NOTE]
> <span data-ttu-id="523d9-110">U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op het beheerde domein die u hebt gemaakt met behulp van Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="523d9-110">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="523d9-111">Op de beheerde domeinen, worden deze machtigingen zijn gereserveerd door de service en zijn niet beschikbaar gesteld aan gebruikers van de tenant.</span><span class="sxs-lookup"><span data-stu-id="523d9-111">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="523d9-112">Echter kunt u de speciale beheergroep gemaakt in deze taak voor de configuratie kunt u sommige bevoorrechte bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="523d9-112">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="523d9-113">Deze bewerkingen zijn computers toevoegen aan het domein en Groepsbeleid configureren die deel uitmaken van de beheergroep op domein-machines.</span><span class="sxs-lookup"><span data-stu-id="523d9-113">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="523d9-114">Maakt de wizard automatisch de beheergroep in uw Azure AD-directory.</span><span class="sxs-lookup"><span data-stu-id="523d9-114">The wizard automatically creates the administrative group in your Azure AD directory.</span></span> <span data-ttu-id="523d9-115">Deze groep wordt 'AAD DC-beheerders' genoemd.</span><span class="sxs-lookup"><span data-stu-id="523d9-115">This group is called 'AAD DC Administrators'.</span></span> <span data-ttu-id="523d9-116">Als u een bestaande groep met deze naam in uw Azure AD-directory hebt, wordt in de wizard deze groep selecteert.</span><span class="sxs-lookup"><span data-stu-id="523d9-116">If you have an existing group with this name in your Azure AD directory, the wizard selects this group.</span></span> <span data-ttu-id="523d9-117">U kunt configureren groepslidmaatschap met de **beheerdersgroep** wizardpagina.</span><span class="sxs-lookup"><span data-stu-id="523d9-117">You can configure group membership using the **Administrator group** wizard page.</span></span>

1. <span data-ttu-id="523d9-118">Voor het configureren van groepslidmaatschap, klikt u op **AAD DC beheerders**.</span><span class="sxs-lookup"><span data-stu-id="523d9-118">To configure group membership, click **AAD DC Administrators**.</span></span>

    ![Groepslidmaatschap configureren](./media/getting-started/domain-services-blade-admingroup.png)

2. <span data-ttu-id="523d9-120">Klik op de **leden toevoegen** knop gebruikers van uw Azure AD-directory toevoegen aan de groep Administrators.</span><span class="sxs-lookup"><span data-stu-id="523d9-120">Click the **Add members** button to add users from your Azure AD directory to the administrator group.</span></span>

3. <span data-ttu-id="523d9-121">Wanneer u klaar bent, klikt u op **OK** op naar de **samenvatting** pagina van de wizard.</span><span class="sxs-lookup"><span data-stu-id="523d9-121">When you are done, click **OK** to move on to the **Summary** page of the wizard.</span></span>

4. <span data-ttu-id="523d9-122">Op de **samenvatting** pagina van de wizard controleert u de configuratie-instellingen voor het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="523d9-122">On the **Summary** page of the wizard, review the configuration settings for the managed domain.</span></span> <span data-ttu-id="523d9-123">U kunt teruggaan naar elke stap van de wizard te wijzigen, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="523d9-123">You can go back to any step of the wizard to make changes, if necessary.</span></span> <span data-ttu-id="523d9-124">Wanneer u klaar bent, klikt u op **OK** om de nieuwe beheerde domein te maken.</span><span class="sxs-lookup"><span data-stu-id="523d9-124">When you are done, click **OK** to create the new managed domain.</span></span>

    ![Samenvatting](./media/getting-started/domain-services-blade-summary.png)

5. <span data-ttu-id="523d9-126">U ziet een melding dat de voortgang van uw Azure AD Domain Services-implementatie geeft.</span><span class="sxs-lookup"><span data-stu-id="523d9-126">You see a notification that shows the progress of your Azure AD Domain Services deployment.</span></span> <span data-ttu-id="523d9-127">Klik op de melding om te zien van gedetailleerde uitgevoerd voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="523d9-127">Click the notification to see detailed progress for the deployment.</span></span>

    ![Melding - implementatie wordt uitgevoerd](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a><span data-ttu-id="523d9-129">Inrichten van uw beheerde domein</span><span class="sxs-lookup"><span data-stu-id="523d9-129">Provision your managed domain</span></span>
<span data-ttu-id="523d9-130">Het proces voor het leveren van uw beheerde domein kan een uur duren.</span><span class="sxs-lookup"><span data-stu-id="523d9-130">The process of provisioning your managed domain can take up to an hour.</span></span>

1. <span data-ttu-id="523d9-131">Tijdens de implementatie uitgevoerd wordt, kunt u zoeken naar 'domeinservices' in de **zoeken bronnen** zoekvak.</span><span class="sxs-lookup"><span data-stu-id="523d9-131">While your deployment is in progress, you can search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="523d9-132">Selecteer **Azure AD Domain Services** uit de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="523d9-132">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="523d9-133">De **Azure AD Domain Services** blade geeft een lijst van het beheerde domein dat wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="523d9-133">The **Azure AD Domain Services** blade lists the managed domain that is being provisioned.</span></span>

    ![Zoeken naar beheerde domein wordt ingericht](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="523d9-135">Klik op de naam van het beheerde domein (bijvoorbeeld, contoso100.com') voor meer informatie over het domein.</span><span class="sxs-lookup"><span data-stu-id="523d9-135">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services - status voor inrichten heeft](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="523d9-137">De **overzicht** tabblad ziet u dat het domein momenteel wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="523d9-137">The **Overview** tab shows that the domain is currently being provisioned.</span></span> <span data-ttu-id="523d9-138">U kunt het beheerde domein niet configureren, totdat deze volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="523d9-138">You cannot configure the managed domain until it is fully provisioned.</span></span> <span data-ttu-id="523d9-139">Dit kan een uur duren voor uw beheerde domein om te worden volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="523d9-139">It may take up to an hour for your managed domain to be fully provisioned.</span></span>

    ![<span data-ttu-id="523d9-140">Domain Services - tabblad Overzicht tijdens de Inrichtingsstatus</span><span class="sxs-lookup"><span data-stu-id="523d9-140">Domain Services - Overview tab during the provisioning state</span></span> ](./media/getting-started/domain-services-provisioning-state-details.png)

4. <span data-ttu-id="523d9-141">Wanneer het beheerde domein volledig is ingericht, de **overzicht** tabblad ziet u de status van het domein als **met**.</span><span class="sxs-lookup"><span data-stu-id="523d9-141">When the managed domain is fully provisioned, the **Overview** tab shows the domain status as **Running**.</span></span>

    ![Domain Services: tabblad Overzicht nadat het domein volledig is ingericht](./media/getting-started/domain-services-provisioned.png)

5. <span data-ttu-id="523d9-143">Op de **eigenschappen** tabblad ziet u twee IP-adressen op welk domein domeincontrollers beschikbaar voor het virtuele netwerk zijn.</span><span class="sxs-lookup"><span data-stu-id="523d9-143">On the **Properties** tab, you see two IP addresses at which domain controllers are available for the virtual network.</span></span>

    ![Domain Services - tabblad Eigenschappen nadat het volledig is ingericht](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a><span data-ttu-id="523d9-145">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="523d9-145">Next step</span></span>
[<span data-ttu-id="523d9-146">Taak 4: DNS-instellingen bijwerken voor het virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="523d9-146">Task 4: update the DNS settings for the Azure virtual network</span></span>](active-directory-ds-getting-started-dns.md)
