---
title: aaaAdd nieuwe gebruikers tooAzure Active Directory | Microsoft Docs
description: Legt uit hoe tooadd nieuwe gebruikers in Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="2d31e-103">Snelstartgids: Nieuwe gebruikers tooAzure Active Directory toevoegen</span><span class="sxs-lookup"><span data-stu-id="2d31e-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="2d31e-104">Dit artikel wordt uitgelegd hoe nieuwe gebruikers in uw organisatie in Azure Active Directory (Azure AD) Hallo tooadd één tegelijk met hello Azure-portal of door het synchroniseren van uw on-premises Windows Server AD-gebruiker account gegevens.</span><span class="sxs-lookup"><span data-stu-id="2d31e-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="2d31e-105">Cloud-gebaseerde gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="2d31e-105">Add cloud-based users</span></span>
1. <span data-ttu-id="2d31e-106">Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="2d31e-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="2d31e-107">Selecteer **Azure Active Directory** en vervolgens **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2d31e-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="2d31e-108">Op Hallo **gebruikers en groepen** blade Selecteer **alle gebruikers**, en selecteer vervolgens **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="2d31e-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="2d31e-109">![Hallo Add-opdracht selecteren](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="2d31e-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="2d31e-110">Voer details voor de gebruiker hello, zoals **naam** en **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="2d31e-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="2d31e-111">Hallo domeingedeelte van gebruikersnaam Hallo moet zijn Hallo initiële standaard domain name '[domeinnaam].onmicrosoft.com' of een geverifieerde niet-gefedereerde [aangepaste domeinnaam](add-custom-domain.md) zoals 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="2d31e-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="2d31e-112">Kopiëren of anderszins Opmerking Hallo gegenereerd gebruikerswachtwoord zodat u deze informatie toohello gebruiker verstrekt kunt nadat dit proces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="2d31e-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="2d31e-113">U kunt desgewenst openen en Hallo gegevens invult in Hallo **profiel** blade, Hallo **groepen** blade of Hallo **functie Directory** blade voor Hallo gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2d31e-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="2d31e-114">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="2d31e-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="2d31e-115">Op Hallo **gebruiker** blade Selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="2d31e-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="2d31e-116">Hallo gegenereerd wachtwoord toohello nieuwe gebruiker veilig distribueren zodat hello gebruiker kunt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="2d31e-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="2d31e-117">U kunt ook gegevens van gebruikersaccounts uit de lokale Windows Server AD synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="2d31e-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="2d31e-118">Microsoft identiteitsoplossingen span on-premises en cloud-gebaseerde mogelijkheden tooall netwerkbronnen, ongeacht de locatie van de identiteit van een enkele gebruiker voor verificatie en autorisatie maken.</span><span class="sxs-lookup"><span data-stu-id="2d31e-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="2d31e-119">We noemen deze hybride identiteit.</span><span class="sxs-lookup"><span data-stu-id="2d31e-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="2d31e-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) gebruikte toointegrate uw on-premises adreslijsten met Azure Active Directory voor hybride identiteit scenario's kan worden.</span><span class="sxs-lookup"><span data-stu-id="2d31e-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="2d31e-121">Hiermee kunt u een algemene identiteit voor uw gebruikers voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide.</span><span class="sxs-lookup"><span data-stu-id="2d31e-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="2d31e-122">Gebruikers verwijderen van Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d31e-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="2d31e-123">Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="2d31e-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="2d31e-124">Selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2d31e-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="2d31e-125">Op Hallo **gebruikers en groepen** blade, selecteer Hallo gebruiker toodelete uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="2d31e-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="2d31e-126">Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **overzicht**, en selecteer vervolgens in de opdrachtbalk Hallo **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2d31e-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="2d31e-127">![Hallo Add-opdracht selecteren](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="2d31e-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="2d31e-128">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="2d31e-128">Learn more</span></span> 
* [<span data-ttu-id="2d31e-129">Een externe gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="2d31e-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="2d31e-130">Een gebruikersrol tooa toewijzen in uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d31e-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="2d31e-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d31e-131">Next steps</span></span>
<span data-ttu-id="2d31e-132">In deze snelstartgids hebt u geleerd hoe tooadd nieuwe gebruikers tooAzure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="2d31e-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="2d31e-133">U kunt Hallo volgende koppeling toocreate een nieuwe gebruiker in Azure AD uit hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2d31e-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d31e-134">Toevoegen van gebruikers tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="2d31e-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
