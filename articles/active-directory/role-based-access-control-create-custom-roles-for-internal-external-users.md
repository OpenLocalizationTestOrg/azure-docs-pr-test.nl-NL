---
title: Aangepaste functies voor toegangsbeheer op basis van rollen maken en toewijzen aan de interne en externe gebruikers in Azure | Microsoft Docs
description: Aangepaste RBAC-rollen gemaakt met behulp van PowerShell en CLI voor interne en externe gebruikers toewijzen
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="1e225-103">Inleiding op rollen gebaseerd toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="1e225-103">Intro on role-based access control</span></span>

<span data-ttu-id="1e225-104">Toegangsbeheer op basis van rollen is een Azure portal alleen functie waardoor de eigenaren van een abonnement gedetailleerde rollen toewijzen aan andere gebruikers die een specifieke bron scopes in hun omgeving kunnen beheren.</span><span class="sxs-lookup"><span data-stu-id="1e225-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="1e225-105">RBAC kunt beter beveiligingsbeheer voor grote organisaties en voor midden-en kleinbedrijf werkt met externe deelnemers, leveranciers of freelancers die toegang tot specifieke bronnen in uw omgeving, maar niet per se aan de gehele infrastructuur of alle scopes facturering-gerelateerde nodig.</span><span class="sxs-lookup"><span data-stu-id="1e225-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="1e225-106">RBAC kunt de flexibiliteit van die eigenaar is van één Azure-abonnement beheerd door de administrator-account (service-beheerdersrol op abonnementsniveau) en hebben meerdere gebruikers uitgenodigd onder hetzelfde abonnement, maar zonder Administrator-rechten voor het werken.</span><span class="sxs-lookup"><span data-stu-id="1e225-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="1e225-107">Vanuit een management en facturering perspectief wordt de functie RBAC blijkt te zijn van een tijd- en efficiënte optie voor het gebruik van Azure in verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="1e225-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e225-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1e225-108">Prerequisites</span></span>
<span data-ttu-id="1e225-109">Het gebruik van RBAC in de Azure-omgeving vereist:</span><span class="sxs-lookup"><span data-stu-id="1e225-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="1e225-110">Een zelfstandige met Azure-abonnement aan de gebruiker toegewezen als eigenaar (abonnement rol)</span><span class="sxs-lookup"><span data-stu-id="1e225-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="1e225-111">De rol van eigenaar van het Azure-abonnement hebt</span><span class="sxs-lookup"><span data-stu-id="1e225-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="1e225-112">Toegang tot de [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1e225-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="1e225-113">Zorg ervoor dat u hebt de volgende Resource Providers geregistreerd voor het abonnement van de gebruiker: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="1e225-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="1e225-114">Zie voor meer informatie over het registreren van de resourceproviders [Resource Manager-providers, regio's, API-versies en schema's](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="1e225-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1e225-115">Abonnementen voor Office 365 of Azure Active Directory-licenties (bijvoorbeeld: toegang tot Azure Active Directory) vanaf de portal niet kwaliteit voor met RBAC O365 wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="1e225-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="1e225-116">Hoe RBAC kan worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="1e225-116">How can RBAC be used</span></span>
<span data-ttu-id="1e225-117">RBAC kan worden toegepast op drie verschillende bereiken in Azure.</span><span class="sxs-lookup"><span data-stu-id="1e225-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="1e225-118">Van het hoogste bereik met de laagste zijn ze als volgt:</span><span class="sxs-lookup"><span data-stu-id="1e225-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="1e225-119">Abonnement (hoogste)</span><span class="sxs-lookup"><span data-stu-id="1e225-119">Subscription (highest)</span></span>
* <span data-ttu-id="1e225-120">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="1e225-120">Resource group</span></span>
* <span data-ttu-id="1e225-121">Resource-bereik (het laagste toegangsniveau aanbieding gerichte machtigingen voor het bereik van een afzonderlijke Azure-resource)</span><span class="sxs-lookup"><span data-stu-id="1e225-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="1e225-122">RBAC-rollen op de scope abonnement toewijzen</span><span class="sxs-lookup"><span data-stu-id="1e225-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="1e225-123">Er zijn twee algemene voorbeelden wanneer RBAC is gebruikt (maar niet tot beperkt):</span><span class="sxs-lookup"><span data-stu-id="1e225-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="1e225-124">Externe gebruikers van de organisaties hebben (die geen deel uit van de gebruiker admin Azure Active Directory-tenant) uitgenodigd om bepaalde bronnen of het hele abonnement te beheren</span><span class="sxs-lookup"><span data-stu-id="1e225-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="1e225-125">Werken met gebruikers binnen de organisatie (ze zijn onderdeel van de gebruiker Azure Active Directory-tenant), maar deel uitmaken van verschillende teams of groepen die gedetailleerde toegang tot het hele abonnement of bepaalde resourcegroepen of resource-scopes in de omgeving nodig</span><span class="sxs-lookup"><span data-stu-id="1e225-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="1e225-126">Toegang verlenen op het abonnementsniveau van een voor een gebruiker buiten Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e225-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="1e225-127">RBAC-rollen kunnen alleen worden toegekend **eigenaars** van het abonnement daarom de gebruiker met beheerdersrechten moet zijn aangemeld met een gebruikersnaam die heeft deze een vooraf toegewezen rol of het Azure-abonnement is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e225-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="1e225-128">Nadat u aanmelden als beheerder, selecteert u vanuit de Azure-portal 'Abonnementen' in en kies de gewenste versie.</span><span class="sxs-lookup"><span data-stu-id="1e225-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="1e225-129">![abonnementsblade in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) standaard als het Azure-abonnement heeft aangeschaft door de gebruiker met beheerdersrechten de gebruiker wordt weergegeven als **accountbeheerder**, dit wordt de rol van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e225-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="1e225-130">Zie voor meer informatie over de functies van Azure-abonnement, [toevoegen of wijzigen Azure-beheerdersrollen die het abonnement of de services beheren](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="1e225-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="1e225-131">In dit voorbeeld wordt de gebruiker "alflanigan@outlook.com' is de **eigenaar** van de 'gratis proefversie' abonnement in het AAD-tenant 'tenant Azure Default'.</span><span class="sxs-lookup"><span data-stu-id="1e225-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="1e225-132">Omdat deze gebruiker de maker van het Azure-abonnement met de eerste 'Outlook' van de Microsoft-Account (Microsoft-Account = Outlook, etc. Live) naam van het standaarddomein voor andere gebruikers die zijn toegevoegd aan deze tenant zijn **'@alflaniganuoutlook.onmicrosoft.com'**.</span><span class="sxs-lookup"><span data-stu-id="1e225-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="1e225-133">Door het ontwerp van de syntaxis van het nieuwe domein wordt gevormd door het samenstellen van de naam van de gebruikersnaam en het domein van de gebruiker die de tenant wordt gemaakt en het toevoegen van de extensie **'. onmicrosoft.com '**.</span><span class="sxs-lookup"><span data-stu-id="1e225-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="1e225-134">Bovendien gebruikers kunnen aanmelden met een aangepaste domeinnaam in de tenant na het toevoegen van en controle van de voor de nieuwe tenant.</span><span class="sxs-lookup"><span data-stu-id="1e225-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="1e225-135">Zie voor meer informatie over het controleren van een aangepaste domeinnaam in een Azure Active Directory-tenant [een aangepaste domeinnaam toevoegen aan uw directory](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="1e225-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="1e225-136">In dit voorbeeld bevat de "standaard Azure ' tenantmap alleen gebruikers met de naam van het domein '@alflanigan.onmicrosoft.com'.</span><span class="sxs-lookup"><span data-stu-id="1e225-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="1e225-137">Na het selecteren van het abonnement, de gebruiker met beheerdersrechten moet op **Access Control (IAM)** en vervolgens **een nieuwe rol toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e225-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![onderdeel voor toegangsbeheer IAM-functie in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![nieuwe gebruiker toevoegen in het onderdeel voor toegangsbeheer IAM-functie in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="1e225-140">De volgende stap is het selecteren van de functie moet worden toegewezen en de gebruiker waaraan de RBAC-rol wordt toegewezen aan.</span><span class="sxs-lookup"><span data-stu-id="1e225-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="1e225-141">In de **rol** het vervolgmenu van de gebruiker met beheerdersrechten ziet alleen de ingebouwde rollen RBAC die beschikbaar in Azure zijn.</span><span class="sxs-lookup"><span data-stu-id="1e225-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="1e225-142">Zie voor meer uitleg van elke rol en hun toewijsbare bereiken gedetailleerde, [ingebouwde functies voor op rollen gebaseerd toegangsbeheer](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1e225-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="1e225-143">De gebruiker met beheerdersrechten moet de e-mailadres van de externe gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1e225-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="1e225-144">Het verwachte gedrag is voor de externe gebruiker worden niet weergegeven in de bestaande tenant.</span><span class="sxs-lookup"><span data-stu-id="1e225-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="1e225-145">Nadat de externe gebruiker heeft uitgenodigd, hij zijn zichtbaar onder **abonnementen > Access Control (IAM)** met de huidige gebruikers dat momenteel een RBAC-rol op het bereik van het abonnement zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1e225-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![Voeg machtigingen toe aan het nieuwe RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![lijst met RBAC-rollen op abonnementsniveau](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="1e225-148">De gebruiker "chessercarlton@gmail.com' heeft uitgenodigd om deel te worden een **eigenaar** voor het abonnement 'Gratis'.</span><span class="sxs-lookup"><span data-stu-id="1e225-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="1e225-149">De externe gebruiker ontvangt een e-mailbevestiging met een activeringskoppeling, na het verzenden van de uitnodiging.</span><span class="sxs-lookup"><span data-stu-id="1e225-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="1e225-150">![e-uitnodiging voor RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="1e225-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="1e225-151">Alleen buiten de organisatie, heeft de nieuwe gebruiker geen bestaande kenmerken in de tenantmap 'Standaard Azure'.</span><span class="sxs-lookup"><span data-stu-id="1e225-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="1e225-152">Ze worden gemaakt nadat de externe gebruiker toestemming heeft gegeven moeten worden vastgelegd in de map die is gekoppeld aan het abonnement dat hij een rol is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1e225-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![e-mailbericht uitnodiging voor RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="1e225-154">De externe gebruiker wordt weergegeven in de Azure Active Directory-tenant op als de externe gebruiker en deze kunnen worden weergegeven in de Azure-portal en in de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="1e225-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![gebruikers blade azure active directory Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![gebruikers blade azure active directory klassieke Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="1e225-157">In de **gebruikers** weergave in beide portals de externe gebruikers kunnen worden herkend door:</span><span class="sxs-lookup"><span data-stu-id="1e225-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="1e225-158">Het type ander pictogram in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="1e225-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="1e225-159">Het andere sourcing punt in de klassieke portal</span><span class="sxs-lookup"><span data-stu-id="1e225-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="1e225-160">Echter verlenen **eigenaar** of **Inzender** toegang tot een externe gebruiker op de **abonnement** bereik, staat niet toe dat de toegang tot de admin gebruikerslijst, tenzij de **globale beheerder** is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="1e225-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="1e225-161">In de eigenschappen van de gebruiker, de **gebruikerstype** die heeft twee algemene parameters, **lid** en **Gast** kunnen worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="1e225-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="1e225-162">Een lid is van een gebruiker die is geregistreerd in de map terwijl een gast een gebruiker uitgenodigd voor de map van een externe bron is.</span><span class="sxs-lookup"><span data-stu-id="1e225-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="1e225-163">Zie voor meer informatie [hoe Azure Active Directory-beheerders Voeg B2B-samenwerking gebruikers](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="1e225-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="1e225-164">Zorg ervoor dat na het invoeren van de referenties in de portal, de externe gebruiker de juiste map aan te melden om te worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1e225-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="1e225-165">Dezelfde gebruiker kan toegang hebben tot meerdere directory's en selecteer een van deze door te klikken op de gebruikersnaam in de rechterbovenhoek in de Azure portal en kies vervolgens de juiste map in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="1e225-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="1e225-166">Terwijl een gast in de directory, de externe gebruiker alle resources voor het Azure-abonnement kunt beheren, maar heeft geen toegang tot de map.</span><span class="sxs-lookup"><span data-stu-id="1e225-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![toegang beperkt tot azure active directory-Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="1e225-168">Azure Active Directory en een Azure-abonnement niet hebben een relatie van de onderliggende structuur met bovenliggende net als andere Azure-resources (bijvoorbeeld: virtuele machines, virtuele netwerken, web-apps, opslag, enzovoort) met een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="1e225-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="1e225-169">Alle deze is gemaakt, beheerd en onder een Azure-abonnement in rekening gebracht terwijl een Azure-abonnement wordt gebruikt voor het beheren van de toegang tot een Azure-map.</span><span class="sxs-lookup"><span data-stu-id="1e225-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="1e225-170">Zie voor meer informatie [hoe een Azure-abonnement is gerelateerd aan Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="1e225-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="1e225-171">Van alle ingebouwde RBAC rollen, **eigenaar** en **Inzender** bieden volledige beheertoegang tot alle bronnen in de omgeving, het verschil is dat een medewerker kan geen maken en nieuwe RBAC-rollen te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1e225-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="1e225-172">De ingebouwde rollen, zoals **Virtual Machine Contributor** bieden volledige management alleen toegang tot de resources die zijn aangegeven door de naam, ongeacht de **resourcegroep** ze worden gemaakt in.</span><span class="sxs-lookup"><span data-stu-id="1e225-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="1e225-173">Toewijzen van de ingebouwde RBAC-rol van **Virtual Machine Contributor** op abonnementsniveau, betekent dit dat de gebruiker de rol toegewezen:</span><span class="sxs-lookup"><span data-stu-id="1e225-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="1e225-174">Kan alle virtuele machines ongeacht hun datum van de implementatie en weergeven ze deel van uitmaken resourcegroepen</span><span class="sxs-lookup"><span data-stu-id="1e225-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="1e225-175">Volledig beheertoegang heeft tot de virtuele machines in het abonnement</span><span class="sxs-lookup"><span data-stu-id="1e225-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="1e225-176">Andere brontypen weergeven in het abonnement niet</span><span class="sxs-lookup"><span data-stu-id="1e225-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="1e225-177">Kan niet worden uitgevoerd vanuit het oogpunt van facturering van wijzigingen</span><span class="sxs-lookup"><span data-stu-id="1e225-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="1e225-178">RBAC wordt een enige functie van Azure portal, verlenen geen toegang tot de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="1e225-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="1e225-179">Een ingebouwde RBAC-rol toewijzen aan een externe gebruiker</span><span class="sxs-lookup"><span data-stu-id="1e225-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="1e225-180">Voor een ander scenario in deze test de externe gebruiker "alflanigan@gmail.com' wordt toegevoegd als een **Virtual Machine Contributor**.</span><span class="sxs-lookup"><span data-stu-id="1e225-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![virtuele machine ingebouwde rol van Inzender](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="1e225-182">Het normale gedrag voor deze externe gebruiker met deze ingebouwde functie is om te zien en beheren van alleen virtuele machines en hun aangrenzende Resource Manager alleen bronnen nodig zijn tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="1e225-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="1e225-183">Standaard bieden deze rollen beperkt alleen toegang tot hun bijbehorende resources in de Azure-portal hebt gemaakt, ongeacht sommige kunnen nog steeds worden geïmplementeerd in de klassieke portal ook (bijvoorbeeld: virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="1e225-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![overzicht van virtuele machines Inzender rol in azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="1e225-185">Toegang verlenen op het abonnementsniveau van een voor een gebruiker in dezelfde map</span><span class="sxs-lookup"><span data-stu-id="1e225-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="1e225-186">De processtroom identiek is aan een externe gebruiker toe te voegen, zowel vanuit het perspectief beheerder is de RBAC-rol, evenals de gebruiker verlenen hun toegang wordt verleend aan de rol.</span><span class="sxs-lookup"><span data-stu-id="1e225-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="1e225-187">Het verschil is hier is dat uitgenodigde de gebruiker niet alle e-uitnodigingen ontvangt als de resource-scopes in het abonnement beschikbaar in het dashboard zijn na het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="1e225-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="1e225-188">RBAC-rollen op het groepsbereik resource toewijzen</span><span class="sxs-lookup"><span data-stu-id="1e225-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="1e225-189">Toewijzen van een RBAC-rol op een **resourcegroep** scope heeft een identieke proces voor het toewijzen van de rol op het abonnementsniveau voor beide typen gebruikers - externe of interne (onderdeel van dezelfde directory).</span><span class="sxs-lookup"><span data-stu-id="1e225-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="1e225-190">De gebruikers die zijn toegewezen de RBAC-rol is om te zien in hun omgeving alleen de resourcegroep waarin ze zijn toegewezen toegang vanaf de **resourcegroepen** pictogram in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1e225-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="1e225-191">RBAC-rollen op het bereik van de resource toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="1e225-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="1e225-192">Toewijzen van een RBAC-rol op een scope resource in Azure heeft een identieke proces voor het toewijzen van de rol op het abonnementsniveau of op het niveau van de resourcegroep, dezelfde werkstroom voor beide scenario's te volgen.</span><span class="sxs-lookup"><span data-stu-id="1e225-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="1e225-193">De gebruikers die de RBAC-rol is toegewezen Zie opnieuw kunnen alleen de items die ze toegang zijn toegewezen aan in de **alle Resources** tabblad of rechtstreeks in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="1e225-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="1e225-194">Er is een belangrijk aspect voor RBAC zowel op resource groepsbereik of resource-bereik voor de gebruikers om ervoor te zorgen voor aanmelden bij de juiste map.</span><span class="sxs-lookup"><span data-stu-id="1e225-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![Directory-aanmelding in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="1e225-196">RBAC-rollen voor een Azure Active Directory-groep toewijzen</span><span class="sxs-lookup"><span data-stu-id="1e225-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="1e225-197">Alle scenario's die gebruikmaken van RBAC op de drie verschillende bereiken in Azure bieden de bevoegdheid beheren, implementeren en beheren van verschillende bronnen als een toegewezen gebruiker zonder de noodzaak om een persoonlijke abonnement te beheren.</span><span class="sxs-lookup"><span data-stu-id="1e225-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="1e225-198">Ongeacht is de RBAC-rol toegewezen voor een abonnement, resourcegroep of resource-bereik, alle zijn onder de één Azure-abonnement waar gebruikers toegang tot hebben de resources verder gemaakt door de toegewezen gebruikers kosten in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="1e225-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="1e225-199">Op deze manier de gebruikers die beschikken over beheerdersrechten voor die volledige Azure-abonnement facturering heeft een volledig overzicht over het verbruik ongeacht wie de resources wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="1e225-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="1e225-200">Voor grotere organisaties, kunnen de RBAC-rollen worden toegepast op dezelfde manier voor het perspectief dat de gebruiker met beheerdersrechten toegang wil verlenen de gedetailleerde voor teams of volledige afdelingen, niet afzonderlijk voor elke gebruiker, overweegt het dus als een zeer tijd- en efficiënte optie overweegt Azure Active Directory-groepen.</span><span class="sxs-lookup"><span data-stu-id="1e225-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="1e225-201">Ter illustratie van dit voorbeeld wordt de **Inzender** rol is toegevoegd aan een van de groepen in de tenant op het abonnementsniveau.</span><span class="sxs-lookup"><span data-stu-id="1e225-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![RBAC-rol voor AAD-groepen toevoegen](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="1e225-203">Deze groepen zijn beveiligingsgroepen die zijn ingericht en beheerd alleen binnen Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e225-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="1e225-204">Maakt een aangepaste RBAC-rol om te openen met behulp van PowerShell ondersteuningsaanvragen</span><span class="sxs-lookup"><span data-stu-id="1e225-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="1e225-205">De ingebouwde RBAC-rollen die beschikbaar in Azure zijn ervoor zorgen dat bepaalde machtigingsniveaus op basis van de beschikbare bronnen in de omgeving.</span><span class="sxs-lookup"><span data-stu-id="1e225-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="1e225-206">Als geen van deze rollen behoeften van de gebruiker admin, is er echter de optie voor het beperken van toegang nog meer door aangepaste RBAC-rollen te maken.</span><span class="sxs-lookup"><span data-stu-id="1e225-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="1e225-207">Maken van aangepaste RBAC-rollen moet een ingebouwde functie, bewerken en vervolgens importeren in de omgeving.</span><span class="sxs-lookup"><span data-stu-id="1e225-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="1e225-208">Het downloaden en het uploaden van de rol worden beheerd met PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="1e225-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="1e225-209">Het is belangrijk om te begrijpen van de vereisten voor het maken van een aangepaste rol die u kunnen gedetailleerde toegang verlenen op het abonnementsniveau en kan de uitgenodigde gebruiker de flexibiliteit ondersteuningsaanvragen te openen.</span><span class="sxs-lookup"><span data-stu-id="1e225-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="1e225-210">In dit voorbeeld de ingebouwde functie **lezer** waarmee gebruikers toegang om alle scopes van de resource weer te geven, maar niet te bewerken of maakt u nieuwe is aangepast om de gebruiker de optie ondersteuningsaanvragen te openen.</span><span class="sxs-lookup"><span data-stu-id="1e225-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="1e225-211">De eerste actie van het exporteren van de **lezer** rol moet worden uitgevoerd in PowerShell met verhoogde machtigingen worden uitgevoerd als administrator.</span><span class="sxs-lookup"><span data-stu-id="1e225-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Schermopname van PowerShell voor de rol Lezer RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="1e225-213">Vervolgens moet u het JSON-sjabloon van de rol extraheren.</span><span class="sxs-lookup"><span data-stu-id="1e225-213">Then you need to extract the JSON template of the role.</span></span>





![JSON-sjabloon voor aangepaste lezer RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="1e225-215">Een typische RBAC-rol bestaat uit drie gedeelten **acties**, **NotActions** en **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="1e225-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="1e225-216">In de **actie** sectie worden de toegestane bewerkingen voor deze rol wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="1e225-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="1e225-217">Het is belangrijk te weten dat elke actie van een resourceprovider is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1e225-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="1e225-218">In dit geval voor het maken van ondersteuningstickets voor van de **Microsoft.Support** resourceprovider moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1e225-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="1e225-219">Om te kunnen zien alle resourceproviders beschikbaar is en geregistreerd in uw abonnement, kunt u PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1e225-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="1e225-220">Bovendien kunt u de alle de beschikbare PowerShell-cmdlets voor het beheren van de resourceproviders controleren.</span><span class="sxs-lookup"><span data-stu-id="1e225-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="1e225-221">![Schermopname van PowerShell voor provider bronbeheer](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="1e225-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="1e225-222">Als u wilt beperken welke acties voor een bepaalde RBAC-rol, resourceproviders worden vermeld in de sectie **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="1e225-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="1e225-223">Laatste, het verplicht is dat de RBAC-rol bevat de expliciete abonnement-id's waar het wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1e225-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="1e225-224">De abonnement-id's worden vermeld in de **AssignableScopes**, anders u niet mag worden importeren van de rol in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e225-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="1e225-225">Na het maken en aanpassen van de RBAC-rol, moet deze worden geïmporteerd back de omgeving.</span><span class="sxs-lookup"><span data-stu-id="1e225-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="1e225-226">In dit voorbeeld is de aangepaste naam voor deze rol RBAC 'Lezer ondersteuning tickets toegangsniveau' zodat de gebruiker kan alles in het abonnement weergeven en openen van aanvragen voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="1e225-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="1e225-227">De slechts twee ingebouwde RBAC-rollen waardoor de actie van het openen van ondersteuningsaanvragen zijn **eigenaar** en **Inzender**.</span><span class="sxs-lookup"><span data-stu-id="1e225-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="1e225-228">Voor een gebruiker om te kunnen openen ondersteuningsaanvragen moet hij worden toegewezen een RBAC-rol alleen op het abonnementsbereik, omdat alle ondersteuningsaanvragen zijn gemaakt op basis van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1e225-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="1e225-229">Deze nieuwe aangepaste rol is toegewezen aan een gebruiker uit dezelfde map.</span><span class="sxs-lookup"><span data-stu-id="1e225-229">This new custom role has been assigned to an user from the same directory.</span></span>





![schermopname van aangepaste RBAC-rol geïmporteerd in de Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![schermopname van het aangepaste geïmporteerde RBAC-rol toewijzen aan gebruiker in dezelfde map](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![schermopname van machtigingen voor aangepaste geïmporteerde RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="1e225-233">In het voorbeeld zijn meer gedetailleerd overzicht te benadrukken de grenzen van deze aangepaste RBAC-rol als volgt:</span><span class="sxs-lookup"><span data-stu-id="1e225-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="1e225-234">Nieuwe ondersteuningsaanvragen kunt maken</span><span class="sxs-lookup"><span data-stu-id="1e225-234">Can create new support requests</span></span>
* <span data-ttu-id="1e225-235">Nieuwe scopes van de resource kan niet worden gemaakt (bijvoorbeeld: virtuele machine)</span><span class="sxs-lookup"><span data-stu-id="1e225-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="1e225-236">Kan de nieuwe resourcegroepen niet maken.</span><span class="sxs-lookup"><span data-stu-id="1e225-236">Can't create new resource groups</span></span>





![schermopname van aangepaste RBAC-rol ondersteuningsaanvragen maken](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![schermopname van aangepaste RBAC-rol kan niet worden gemaakt van virtuele machines](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![schermopname van aangepaste RBAC-rol kan niet worden gemaakt van nieuwe RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="1e225-240">Maakt een aangepaste RBAC-rol om te openen met behulp van Azure CLI ondersteuningsaanvragen</span><span class="sxs-lookup"><span data-stu-id="1e225-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="1e225-241">Azure CLI is uitgevoerd op een Mac en zonder dat toegang tot PowerShell, is de manier om te gaan.</span><span class="sxs-lookup"><span data-stu-id="1e225-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="1e225-242">De stappen voor het maken van een aangepaste beveiligingsrol zijn hetzelfde, met de enige uitzondering die met behulp van de rol CLI in een JSON-sjabloon kan niet worden gedownload, maar deze kan worden weergegeven in de CLI.</span><span class="sxs-lookup"><span data-stu-id="1e225-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="1e225-243">Ik heb de ingebouwde rol van de gekozen voor dit voorbeeld **back-up lezer**.</span><span class="sxs-lookup"><span data-stu-id="1e225-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Schermafbeelding van de rol van back-lezer CLI weergeven](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="1e225-245">De rol in Visual Studio bewerken na het kopiëren van de eigenschappen in een JSON-sjabloon, het **Microsoft.Support** resourceprovider is toegevoegd aan de **acties** secties zodat deze gebruiker ondersteuningsaanvragen openen kunt terwijl u moet een lezer voor de back-upkluizen.</span><span class="sxs-lookup"><span data-stu-id="1e225-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="1e225-246">Opnieuw is het nodig zijn om toe te voegen van de abonnements-ID waarop u deze rol wordt gebruikt in de **AssignableScopes** sectie.</span><span class="sxs-lookup"><span data-stu-id="1e225-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![CLI-schermopname van het importeren van aangepaste RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="1e225-248">De nieuwe functie is nu beschikbaar in de Azure-portal en de toewijzing-proces is hetzelfde als in de eerdere voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1e225-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![Azure portal schermafbeelding van aangepaste RBAC-rol gemaakt met behulp van de CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="1e225-250">De Azure-Cloud-Shell is vanaf de meest recente Build-2017 algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1e225-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="1e225-251">Azure Cloud-Shell vormt een aanvulling op de IDE- en de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="1e225-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="1e225-252">Met deze service krijgt u een browser gebaseerde shell die is geverifieerd en wordt gehost in Azure en u kunt deze gebruiken in plaats van de CLI op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1e225-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure-Cloud-Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
