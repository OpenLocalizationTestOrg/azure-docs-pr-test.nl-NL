---
title: Nieuwe gebruikers toevoegen aan Azure Active Directory | Microsoft Docs
description: Legt uit hoe u nieuwe gebruikers toevoegen in Azure Active Directory.
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
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="393d6-103">Snelstartgids: Nieuwe gebruikers toevoegen aan Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="393d6-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="393d6-104">In dit artikel wordt uitgelegd hoe u nieuwe gebruikers toevoegen in uw organisatie in Azure Active Directory (Azure AD) een op een tijdstip met de Azure portal of door het synchroniseren van uw on-premises Windows Server AD-gegevens voor account van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="393d6-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="393d6-105">Cloud-gebaseerde gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="393d6-105">Add cloud-based users</span></span>
1. <span data-ttu-id="393d6-106">Aanmelden bij de [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="393d6-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="393d6-107">Selecteer **Azure Active Directory** en vervolgens **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="393d6-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="393d6-108">Op de **gebruikers en groepen** blade Selecteer **alle gebruikers**, en selecteer vervolgens **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="393d6-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="393d6-109">![De opdracht Add selecteren](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="393d6-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="393d6-110">Voer details voor de gebruiker, zoals **naam** en **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="393d6-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="393d6-111">Het domeingedeelte van de naam van de gebruikersnaam moet worden de oorspronkelijke standaard domain name '[domeinnaam].onmicrosoft.com' of een geverifieerde niet-gefedereerde [aangepaste domeinnaam](add-custom-domain.md) zoals 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="393d6-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="393d6-112">Kopieer of het wachtwoord van de gebruiker gegenereerde anders opmerking zodat u deze informatie aan de gebruiker verstrekt kunt nadat dit proces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="393d6-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="393d6-113">U kunt desgewenst openen en vul de informatie in de **profiel** blade de **groepen** blade of de **functie Directory** blade voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="393d6-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="393d6-114">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="393d6-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="393d6-115">Op de **gebruiker** blade Selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="393d6-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="393d6-116">Het gegenereerde wachtwoord naar de nieuwe gebruiker veilig distribueren zodat de gebruiker zich kan aanmelden.</span><span class="sxs-lookup"><span data-stu-id="393d6-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="393d6-117">U kunt ook gegevens van gebruikersaccounts uit de lokale Windows Server AD synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="393d6-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="393d6-118">Microsoft identiteitsoplossingen span on-premises en cloud-gebaseerde mogelijkheden voor het maken van de identiteit van een enkele gebruiker voor verificatie en autorisatie voor alle netwerkbronnen, ongeacht de locatie.</span><span class="sxs-lookup"><span data-stu-id="393d6-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="393d6-119">We noemen deze hybride identiteit.</span><span class="sxs-lookup"><span data-stu-id="393d6-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="393d6-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) kan worden gebruikt om uw on-premises adreslijsten integreren met Azure Active Directory voor hybride identiteit scenario's.</span><span class="sxs-lookup"><span data-stu-id="393d6-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="393d6-121">Hiermee kunt u uw gebruikers een algemene identiteit bieden voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="393d6-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="393d6-122">Gebruikers verwijderen van Azure AD</span><span class="sxs-lookup"><span data-stu-id="393d6-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="393d6-123">Aanmelden bij de [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="393d6-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="393d6-124">Selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="393d6-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="393d6-125">Op de **gebruikers en groepen** blade, selecteer de gebruiker wilt verwijderen uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="393d6-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="393d6-126">Selecteer op de blade voor de geselecteerde gebruiker **overzicht**, en selecteer vervolgens in de opdrachtbalk **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="393d6-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="393d6-127">![De opdracht Add selecteren](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="393d6-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="393d6-128">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="393d6-128">Learn more</span></span> 
* [<span data-ttu-id="393d6-129">Een externe gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="393d6-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="393d6-130">Een gebruiker toewijzen aan een rol in uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="393d6-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="393d6-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="393d6-131">Next steps</span></span>
<span data-ttu-id="393d6-132">In deze snelstartgids hebt u geleerd hoe u nieuwe gebruikers toevoegen aan Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="393d6-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="393d6-133">De volgende koppeling kunt u een nieuwe gebruiker in Azure AD via de Azure portal maken.</span><span class="sxs-lookup"><span data-stu-id="393d6-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="393d6-134">Gebruikers toevoegen aan Azure AD</span><span class="sxs-lookup"><span data-stu-id="393d6-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 