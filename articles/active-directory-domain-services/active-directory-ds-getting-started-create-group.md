---
title: 'Azure Active Directory Domain Services: De Azure AD-DC-beheerdersgroep maken | Microsoft Docs'
description: Azure Active Directory Domain Services inschakelen met behulp van de klassieke Azure-portal
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
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="7373e-103">Azure Active Directory Domain Services inschakelen met behulp van de klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7373e-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="7373e-104">In dit artikel wordt beschreven en wordt begeleid bij de configuratietaken die vereist zijn voor u inschakelen van Azure Active Directory Domain Services (Azure AD DS) voor uw tenant van Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7373e-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="7373e-105">[**Probeer de nieuwe portal (preview) Azure-ervaring in plaats daarvan**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7373e-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="7373e-106">Taak 1: de Azure AD-DC-beheerdersgroep maken</span><span class="sxs-lookup"><span data-stu-id="7373e-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="7373e-107">De eerste taak is het maken van een beheergroep in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="7373e-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="7373e-108">Deze speciale beheerdersgroep heet *AAD DC beheerders*.</span><span class="sxs-lookup"><span data-stu-id="7373e-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="7373e-109">Leden van deze groep worden verleend beheerdersmachtigingen op de computers die zijn met het domein is gekoppeld aan het Azure Active Directory Domain Services beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="7373e-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="7373e-110">Op de machines domein, wordt deze groep toegevoegd aan de groep administrators.</span><span class="sxs-lookup"><span data-stu-id="7373e-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="7373e-111">Leden van deze groep kunnen ook extern bureaublad gebruiken extern verbinding maken met domein-machines.</span><span class="sxs-lookup"><span data-stu-id="7373e-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="7373e-112">U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op het beheerde domein die u hebt gemaakt met behulp van Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7373e-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="7373e-113">Op de beheerde domeinen, worden deze machtigingen zijn gereserveerd door de service en zijn niet beschikbaar gesteld aan gebruikers van de tenant.</span><span class="sxs-lookup"><span data-stu-id="7373e-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="7373e-114">Echter kunt u de speciale beheergroep gemaakt in deze taak voor de configuratie kunt u sommige bevoorrechte bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7373e-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="7373e-115">Deze bewerkingen zijn computers toevoegen aan het domein en Groepsbeleid configureren die deel uitmaken van de beheergroep op domein-machines.</span><span class="sxs-lookup"><span data-stu-id="7373e-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="7373e-116">In deze configuratietaak maken van de beheergroep en een of meer gebruikers in uw directory toevoegen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="7373e-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="7373e-117">Voor het maken van de beheergroep voor Azure Active Directory Domain Services, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7373e-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="7373e-118">Ga naar de [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7373e-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="7373e-119">Selecteer de knop **Active Directory** in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="7373e-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="7373e-120">Selecteer de Azure AD-tenant (directory) waarvoor u wilt inschakelen van Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7373e-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="7373e-121">U kunt slechts één domein voor elke Azure AD-directory maken.</span><span class="sxs-lookup"><span data-stu-id="7373e-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="7373e-123">Op de **preview directory** pagina, klikt u op de **groepen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7373e-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="7373e-124">U voegt een groep toe aan uw Azure AD-tenant in het taakvenster onder aan het venster **groep toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7373e-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![De knop groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="7373e-126">In de **groep toevoegen** dialoogvenster vak, maakt u een groep met de naam **AAD DC beheerders**, en stel vervolgens **groepstype** naar **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="7373e-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="7373e-127">Voor toegang binnen uw Azure Active Directory Domain Services beheerd domein, een groep te maken met deze naam.</span><span class="sxs-lookup"><span data-stu-id="7373e-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![Het dialoogvenster groep toevoegen](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="7373e-129">In de **beschrijving** vak, voer een beschrijving in waarmee anderen om te begrijpen dat deze codegroep beheerdersmachtigingen binnen Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7373e-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="7373e-130">Nadat u de groep hebt gemaakt, klikt u op de naam van de groep om de eigenschappen ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7373e-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="7373e-131">U kunt gebruikers toevoegen als leden van de groep aan de onderkant van het venster op de **leden toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="7373e-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Knop voor leden van groep toevoegen](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="7373e-133">In de **leden toevoegen** dialoogvenster Selecteer de gebruikers die u moeten lid zijn van deze groep en klik vervolgens op het vinkje in de rechterbenedenhoek.</span><span class="sxs-lookup"><span data-stu-id="7373e-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Gebruikers toevoegen aan de groep administrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="7373e-135">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="7373e-135">Next step</span></span>
[<span data-ttu-id="7373e-136">Taak 2: Maak of Selecteer een Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="7373e-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
