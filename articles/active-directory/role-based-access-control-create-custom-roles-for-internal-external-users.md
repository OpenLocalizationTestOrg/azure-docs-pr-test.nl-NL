---
title: aaaCreate aangepaste op rollen gebaseerde toegangsbeheer rollen en toe te wijzen toointernal en externe gebruikers in Azure | Microsoft Docs
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
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="44222-103">Inleiding op rollen gebaseerd toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="44222-103">Intro on role-based access control</span></span>

<span data-ttu-id="44222-104">Toegangsbeheer op basis van rollen is een Azure portal alleen functie zodat Hallo eigenaren van een abonnement tooassign gedetailleerde rollen tooother gebruikers die een specifieke bron scopes in hun omgeving kunnen beheren.</span><span class="sxs-lookup"><span data-stu-id="44222-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="44222-105">RBAC kan beter beveiligingsbeheer voor grote organisaties en voor midden-en kleinbedrijf werkt met externe deelnemers, leveranciers of freelancers die moeten toegang hebben tot bronnen in uw omgeving, maar niet noodzakelijkerwijs toohello gehele infrastructuur of een willekeurige toospecific Facturering-gerelateerde scopes.</span><span class="sxs-lookup"><span data-stu-id="44222-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="44222-106">RBAC kan Hallo flexibiliteit van die eigenaar is van een Azure-abonnement beheerd door Hallo administrator-account (service-beheerdersrol op abonnementsniveau) en hebben meerdere gebruikers uitgenodigd toowork onder Hallo hetzelfde abonnement maar zonder een administratieve rechten voor.</span><span class="sxs-lookup"><span data-stu-id="44222-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="44222-107">Hallo RBAC functie bewijst toobe een tijd- en efficiënte optie voor het gebruik van Azure in verschillende scenario's van een management en facturering perspectief.</span><span class="sxs-lookup"><span data-stu-id="44222-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44222-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="44222-108">Prerequisites</span></span>
<span data-ttu-id="44222-109">Het gebruik van RBAC in hello Azure-omgeving vereist:</span><span class="sxs-lookup"><span data-stu-id="44222-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="44222-110">Een zelfstandige met Azure-abonnement toohello gebruiker toegewezen als eigenaar (abonnement rol)</span><span class="sxs-lookup"><span data-stu-id="44222-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="44222-111">Rol van eigenaar Hallo Hallo Azure-abonnement hebt</span><span class="sxs-lookup"><span data-stu-id="44222-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="44222-112">Hebt u toegang toohello [Azure-portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="44222-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="44222-113">Zorg ervoor dat toohave hello Resourceproviders te volgen die zijn geregistreerd voor Hallo gebruikerabonnement: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="44222-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="44222-114">Zie voor meer informatie over hoe tooregister resourceproviders hello, [Resource Manager-providers, regio's, API-versies en schema's](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="44222-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="44222-115">Abonnementen voor Office 365 of Azure Active Directory-licenties (bijvoorbeeld: toegang tot Active Directory tooAzure) vanaf Hallo O365 portal niet kwaliteit voor met RBAC wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="44222-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="44222-116">Hoe RBAC kan worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="44222-116">How can RBAC be used</span></span>
<span data-ttu-id="44222-117">RBAC kan worden toegepast op drie verschillende bereiken in Azure.</span><span class="sxs-lookup"><span data-stu-id="44222-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="44222-118">Van Hallo hoogste bereik toohello laagste één zijn ze als volgt:</span><span class="sxs-lookup"><span data-stu-id="44222-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="44222-119">Abonnement (hoogste)</span><span class="sxs-lookup"><span data-stu-id="44222-119">Subscription (highest)</span></span>
* <span data-ttu-id="44222-120">Resourcegroep</span><span class="sxs-lookup"><span data-stu-id="44222-120">Resource group</span></span>
* <span data-ttu-id="44222-121">Resource-bereik (Hallo laagste toegangsniveau gerichte machtigingen tooan afzonderlijke Azure-resource bereik aanbieden)</span><span class="sxs-lookup"><span data-stu-id="44222-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="44222-122">RBAC-rollen op Hallo abonnementsbereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="44222-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="44222-123">Er zijn twee algemene voorbeelden wanneer RBAC is gebruikt (maar niet tot beperkt):</span><span class="sxs-lookup"><span data-stu-id="44222-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="44222-124">Externe gebruikers van Hallo organisaties (die geen deel uit van Azure Active Directory-tenant Hallo beheerder van de gebruiker) met uitgenodigd toomanage bepaalde resources of de hele abonnement Hallo</span><span class="sxs-lookup"><span data-stu-id="44222-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="44222-125">Werken met gebruikers binnen het Hallo-organisatie (ze zijn onderdeel van een van de gebruiker hello Azure Active Directory-tenant), maar deel uitmaken van verschillende teams of groepen die gedetailleerde toegang moeten beide toohello hele abonnement of toocertain resourcegroepen of de resource-bereiken in Hallo omgeving</span><span class="sxs-lookup"><span data-stu-id="44222-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="44222-126">Toegang verlenen op het abonnementsniveau van een voor een gebruiker buiten Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44222-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="44222-127">RBAC-rollen kunnen alleen worden toegekend **eigenaars** van Hallo abonnement daarom Hallo beheerder moet zijn aangemeld met een gebruikersnaam die deze rol is een vooraf toegewezen of hello Azure-abonnement is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44222-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="44222-128">Van hello Azure-portal, na het aanmelden als beheerder, selecteer 'Abonnementen' en gekozen Hallo gewenste een.</span><span class="sxs-lookup"><span data-stu-id="44222-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="44222-129">![abonnementsblade in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) standaard als gebruiker met beheerdersrechten Hallo hello Azure-abonnement heeft aangeschaft Hallo gebruiker wordt weergegeven als **accountbeheerder**, deze wordt Hallo abonnement rol.</span><span class="sxs-lookup"><span data-stu-id="44222-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="44222-130">Zie voor meer informatie over hello Azure-abonnement rollen [toevoegen of wijzigen Azure-beheerdersrollen die Hallo abonnement of services beheren](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="44222-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="44222-131">In dit voorbeeld Hallo gebruiker "alflanigan@outlook.com' hello is **eigenaar** Hallo 'Gratis' abonnement in Hallo AAD-tenant 'tenant Azure Default'.</span><span class="sxs-lookup"><span data-stu-id="44222-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="44222-132">Omdat deze gebruiker Hallo maker van hello Azure-abonnement met Hallo initiële Microsoft-Account 'Outlook' (Microsoft-Account = Outlook, etc. Live) Hallo standaarddomeinnaam voor andere gebruikers die zijn toegevoegd aan deze tenant zijn **'@alflaniganuoutlook.onmicrosoft.com'**.</span><span class="sxs-lookup"><span data-stu-id="44222-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="44222-133">Standaard Hallo syntaxis van het nieuwe domein hello wordt gevormd door het samenstellen van Hallo gebruikersnaam en domein op naam van Hallo-gebruiker die Hallo-tenant en toe te voegen Hallo extensie gemaakt **'. onmicrosoft.com '**.</span><span class="sxs-lookup"><span data-stu-id="44222-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="44222-134">Bovendien gebruikers kunnen aanmelden met een aangepaste domeinnaam in Hallo tenant na het toevoegen en verifiëren van deze voor de nieuwe tenant Hallo.</span><span class="sxs-lookup"><span data-stu-id="44222-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="44222-135">Voor meer informatie over hoe tooverify een aangepaste domeinnaam in Azure Active Directory-tenant, Zie [toevoegen van een aangepast domein naam tooyour map](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="44222-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="44222-136">In dit voorbeeld bevat Hallo ' standaard Azure ' tenantmap alleen gebruikers met de domeinnaam Hallo '@alflanigan.onmicrosoft.com'.</span><span class="sxs-lookup"><span data-stu-id="44222-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="44222-137">Na het selecteren van abonnement Hallo Hallo beheerder gebruiker klikt op **Access Control (IAM)** en vervolgens **een nieuwe rol toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="44222-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![onderdeel voor toegangsbeheer IAM-functie in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![nieuwe gebruiker toevoegen in het onderdeel voor toegangsbeheer IAM-functie in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="44222-140">de volgende stap Hallo is tooselect Hallo rol toobe toegewezen en Hallo gebruiker wie Hallo RBAC-rol wordt toegewezen aan.</span><span class="sxs-lookup"><span data-stu-id="44222-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="44222-141">In Hallo **rol** dropdown menu Hallo beheerder gebruiker ziet alleen Hallo ingebouwde RBAC functies die beschikbaar in Azure zijn.</span><span class="sxs-lookup"><span data-stu-id="44222-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="44222-142">Zie voor meer uitleg van elke rol en hun toewijsbare bereiken gedetailleerde, [ingebouwde functies voor op rollen gebaseerd toegangsbeheer](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="44222-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="44222-143">Hallo beheerder gebruiker moet vervolgens tooadd Hallo e-mailadres van de externe gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="44222-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="44222-144">Hallo verwacht gedrag is voor Hallo externe gebruiker toonot worden weergegeven in Hallo bestaande tenant.</span><span class="sxs-lookup"><span data-stu-id="44222-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="44222-145">Nadat de externe gebruiker Hallo heeft uitgenodigd, hij zijn zichtbaar onder **abonnementen > Access Control (IAM)** met alle Hallo actieve gebruikers dat momenteel een RBAC-rol op Hallo abonnementsbereik zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="44222-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![machtigingen toonew RBAC-rol toevoegen](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![lijst met RBAC-rollen op abonnementsniveau](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="44222-148">Hallo-gebruiker 'chessercarlton@gmail.com' uitgenodigde toobe is een **eigenaar** voor Hallo ' gratis ' proefabonnement.</span><span class="sxs-lookup"><span data-stu-id="44222-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="44222-149">Na het verzenden van een uitnodiging voor Hallo ontvangen Hallo externe gebruiker een e-mailbevestiging met een activeringskoppeling.</span><span class="sxs-lookup"><span data-stu-id="44222-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="44222-150">![e-uitnodiging voor RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="44222-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="44222-151">Alleen externe toohello organisatie, heeft Hallo nieuwe gebruiker geen bestaande kenmerken in Hallo 'tenant Azure Default' directory.</span><span class="sxs-lookup"><span data-stu-id="44222-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="44222-152">Ze worden gemaakt nadat de externe gebruiker Hallo heeft toestemming toobe vastgelegd in Hallo directory, die is gekoppeld aan Hallo-abonnement dat hij een rol is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="44222-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![e-mailbericht uitnodiging voor RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="44222-154">ziet u de externe gebruiker Hallo in hello Azure Active Directory-tenant op als de externe gebruiker en deze kan worden bekeken in hello Azure-portal en in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="44222-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![gebruikers blade azure active directory Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![gebruikers blade azure active directory klassieke Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="44222-157">In Hallo **gebruikers** weergave in beide portals Hallo externe gebruikers kan worden herkend door:</span><span class="sxs-lookup"><span data-stu-id="44222-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="44222-158">Hallo ander Pictogramtype in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="44222-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="44222-159">Hallo verschillende punt in de klassieke portal Hallo bron</span><span class="sxs-lookup"><span data-stu-id="44222-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="44222-160">Echter, verlenen **eigenaar** of **Inzender** toegang tooan externe gebruiker op Hallo **abonnement** bereik, staat niet toe dat Hallo toegang toohello-beheerder de map van gebruiker, tenzij Hallo **globale beheerder** is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="44222-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="44222-161">In de eigenschappen van de gebruiker hello, Hallo **gebruikerstype** die heeft twee algemene parameters, **lid** en **Gast** kunnen worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="44222-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="44222-162">Een lid is van een gebruiker die is geregistreerd in de map Hallo terwijl een gast een map van de gebruiker verzocht toohello van een externe bron is.</span><span class="sxs-lookup"><span data-stu-id="44222-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="44222-163">Zie voor meer informatie [hoe Azure Active Directory-beheerders Voeg B2B-samenwerking gebruikers](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="44222-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="44222-164">Zorg ervoor dat de externe gebruiker Hallo na het invoeren van Hallo-referenties in portal Hallo, de juiste map Hallo toosign bij selecteert.</span><span class="sxs-lookup"><span data-stu-id="44222-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="44222-165">Hallo kan dezelfde gebruiker toegang toomultiple mappen hebt en kunt selecteert u een van deze door te klikken op Hallo gebruikersnaam in Hallo rechterbovenhoek in hello Azure-portal en kies vervolgens de overeenkomstige map Hallo uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="44222-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="44222-166">Terwijl een gast in Hallo directory, Hallo externe gebruiker alle resources voor hello Azure-abonnement kunt beheren, maar geen toegang tot Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="44222-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![toegang tot Azure active directory-portal beperkte tooazure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="44222-168">Azure Active Directory en een Azure-abonnement niet hebben een relatie van de onderliggende structuur met bovenliggende net als andere Azure-resources (bijvoorbeeld: virtuele machines, virtuele netwerken, web-apps, opslag, enzovoort) met een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="44222-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="44222-169">Alle Hallo laatstgenoemde is gemaakt, beheerd en onder een Azure-abonnement in rekening gebracht terwijl een Azure-abonnement gebruikte toomanage Hallo toegang tooan Azure-map is.</span><span class="sxs-lookup"><span data-stu-id="44222-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="44222-170">Zie voor meer informatie [hoe een Azure-abonnement is gerelateerd tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="44222-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="44222-171">Uit alle Hallo ingebouwde RBAC rollen, **eigenaar** en **Inzender** bieden volledige beheertoegang tooall bronnen Hallo-omgeving, Hallo verschil wordt die een medewerker kan niet worden gemaakt en nieuwe verwijderen RBAC-rollen.</span><span class="sxs-lookup"><span data-stu-id="44222-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="44222-172">Hallo andere ingebouwde rollen, zoals **Virtual Machine Contributor** bieden volledige beheertoegang alleen toohello resources aangegeven door de naam hello, ongeacht Hallo **resourcegroep** ze worden gemaakt in.</span><span class="sxs-lookup"><span data-stu-id="44222-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="44222-173">Toewijzen Hallo ingebouwde RBAC-rol van **Virtual Machine Contributor** op abonnementsniveau, betekent dat Hallo toegewezen Hallo gebruikersrol:</span><span class="sxs-lookup"><span data-stu-id="44222-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="44222-174">Alle virtuele machines ongeacht hun implementatie van de datum en het Hallo resource-groepen kunt weergeven die ze deel van uitmaken</span><span class="sxs-lookup"><span data-stu-id="44222-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="44222-175">Heeft volledige toegang toohello virtuele beheermachines in Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="44222-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="44222-176">Andere brontypen weergeven in Hallo abonnement niet</span><span class="sxs-lookup"><span data-stu-id="44222-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="44222-177">Kan niet worden uitgevoerd vanuit het oogpunt van facturering van wijzigingen</span><span class="sxs-lookup"><span data-stu-id="44222-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="44222-178">RBAC wordt een enige functie van Azure portal, verlenen geen toegang toohello klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="44222-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="44222-179">Een ingebouwde RBAC-rol tooan externe gebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="44222-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="44222-180">Hallo externe gebruiker voor een ander scenario in deze test 'alflanigan@gmail.com' wordt toegevoegd als een **Virtual Machine Contributor**.</span><span class="sxs-lookup"><span data-stu-id="44222-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![virtuele machine ingebouwde rol van Inzender](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="44222-182">Hallo normaal gedrag voor deze externe gebruiker met deze ingebouwde functie toosee is en alleen virtuele machines en hun aangrenzende Resource Manager alleen bronnen nodig zijn tijdens de implementatie beheren.</span><span class="sxs-lookup"><span data-stu-id="44222-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="44222-183">Door het ontwerp van deze rollen beperkt bieden toegang alleen tootheir corresponderende resources in hello Azure-portal hebt gemaakt, ongeacht sommige kan nog steeds worden geïmplementeerd in Hallo klassieke portal ook (bijvoorbeeld: virtuele machines).</span><span class="sxs-lookup"><span data-stu-id="44222-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![overzicht van virtuele machines Inzender rol in azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="44222-185">Ken toegang tot op het abonnementsniveau van een voor een gebruiker in Hallo dezelfde directory</span><span class="sxs-lookup"><span data-stu-id="44222-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="44222-186">Processtroom Hallo is identiek tooadding een externe gebruiker zowel in Hallo beheerder perspectief verlenen Hallo RBAC-rol, evenals Hallo gebruiker toohello-toegangsfunctie wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="44222-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="44222-187">Hallo verschil is hier is dat die Hallo uitgenodigd gebruiker ontvangt geen uitnodigingen voor een e-mailadres als alle Hallo resource scopes binnen Hallo abonnement beschikbaar in Hallo dashboard zijn na het aanmelden.</span><span class="sxs-lookup"><span data-stu-id="44222-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="44222-188">RBAC-rollen op Hallo resource groepsbereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="44222-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="44222-189">Toewijzen van een RBAC-rol op een **resourcegroep** scope heeft een identieke proces voor het toewijzen van Hallo-rol op Hallo abonnementsniveau, voor beide typen gebruikers - externe of interne (onderdeel van Hallo dezelfde directory).</span><span class="sxs-lookup"><span data-stu-id="44222-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="44222-190">Hallo gebruikers die zijn toegewezen Hallo RBAC-rol is toosee in hun omgeving alleen Hallo resourcegroep ze zijn toegewezen toegang van Hallo **resourcegroepen** pictogram in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="44222-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="44222-191">RBAC-rollen op Hallo resource bereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="44222-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="44222-192">Toewijzen van een RBAC-rol op een scope resource in Azure heeft een identieke proces voor het toewijzen van Hallo-rol op Hallo abonnementsniveau of op niveau van de resourcegroep hello, volgende Hallo dezelfde werkstroom voor beide scenario's.</span><span class="sxs-lookup"><span data-stu-id="44222-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="44222-193">Hallo-gebruikers die zijn toegewezen Hallo RBAC-rol Zie opnieuw kunnen alleen Hallo items dat ze zijn toegewezen toegang op beide in hello **alle Resources** tabblad of rechtstreeks in het dashboard.</span><span class="sxs-lookup"><span data-stu-id="44222-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="44222-194">Een belangrijk aspect voor RBAC zowel op resource groepsbereik of bereik van de resource is voor Hallo gebruikers toomake zeker toosign in toohello correcte directory.</span><span class="sxs-lookup"><span data-stu-id="44222-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![Directory-aanmelding in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="44222-196">RBAC-rollen voor een Azure Active Directory-groep toewijzen</span><span class="sxs-lookup"><span data-stu-id="44222-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="44222-197">Alle Hallo-scenario's met RBAC op drie verschillende bereiken Hallo in Azure-aanbieding Hallo bevoegdheid beheren, implementeren en beheren van verschillende bronnen als een toegewezen gebruiker zonder Hallo moeten van het beheer van een persoonlijke abonnement.</span><span class="sxs-lookup"><span data-stu-id="44222-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="44222-198">Ongeacht Hallo RBAC-rol is toegewezen voor een abonnement, resourcegroep of resource-scope, zijn onder Hallo één Azure-abonnement waarbij Hallo gebruikers toegang tot hebben alle Hallo resources verder gemaakt door Hallo toegewezen gebruikers kosten in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="44222-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="44222-199">Op deze manier hello gebruikers die beschikken over beheerdersrechten voor die volledige Azure-abonnement facturering heeft een volledig overzicht van Hallo verbruik, ongeacht wie Hallo resources wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="44222-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="44222-200">Voor grotere organisaties RBAC-rollen kunnen worden toegepast in Hallo dezelfde manier voor Azure Active Directory-groepen overweegt Hallo perspectief die Hallo beheerder gebruiker toogrant Hallo gedetailleerde toegang wil voor teams of volledige afdelingen, niet afzonderlijk voor elke gebruiker, dus kijken we naar deze als een zeer tijd- en efficiënte optie.</span><span class="sxs-lookup"><span data-stu-id="44222-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="44222-201">tooillustrate in dit voorbeeld, Hallo **Inzender** rol is toegevoegd tooone van Hallo groepen in op abonnementsniveau Hallo Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="44222-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![RBAC-rol voor AAD-groepen toevoegen](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="44222-203">Deze groepen zijn beveiligingsgroepen die zijn ingericht en beheerd alleen binnen Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44222-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="44222-204">Maak een aangepaste RBAC-rol tooopen ondersteuning aanvragen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="44222-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="44222-205">Hallo ingebouwde RBAC-rollen die beschikbaar in Azure zijn ervoor zorgen dat bepaalde machtigingsniveaus op basis van beschikbare resources in de omgeving Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44222-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="44222-206">Als geen van deze rollen Hallo beheerder gebruiker behoeften, is er echter Hallo optie toolimit toegang nog meer door aangepaste RBAC-rollen te maken.</span><span class="sxs-lookup"><span data-stu-id="44222-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="44222-207">Voor het maken van aangepaste RBAC-rollen moet een ingebouwde rol tootake, bewerken en vervolgens importeren in Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="44222-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="44222-208">Hallo downloaden en het uploaden van Hallo rol worden beheerd met PowerShell of CLI.</span><span class="sxs-lookup"><span data-stu-id="44222-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="44222-209">Het is belangrijk toounderstand Hallo vereisten voor het maken van een aangepaste rol die u kunnen gedetailleerde toegang verlenen op abonnementsniveau Hallo en ook de mogelijkheid Hallo uitgenodigd gebruiker Hallo flexibiliteit ondersteuningsaanvragen te openen.</span><span class="sxs-lookup"><span data-stu-id="44222-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="44222-210">Voor dit voorbeeld Hallo ingebouwde rol **lezer** waarmee gebruikers toegang tooview Hallo-resource alle scopes maar niet tooedit ze of nieuwe maken is aangepast tooallow Hallo Hallo optie ondersteuningsaanvragen te openen.</span><span class="sxs-lookup"><span data-stu-id="44222-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="44222-211">eerste actie van het exporteren van Hallo Hallo **lezer** rol behoeften toobe voltooid in PowerShell met verhoogde machtigingen worden uitgevoerd als administrator.</span><span class="sxs-lookup"><span data-stu-id="44222-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Schermopname van PowerShell voor de rol Lezer RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="44222-213">Vervolgens moet u tooextract Hallo JSON-sjabloon van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="44222-213">Then you need tooextract hello JSON template of hello role.</span></span>





![JSON-sjabloon voor aangepaste lezer RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="44222-215">Een typische RBAC-rol bestaat uit drie gedeelten **acties**, **NotActions** en **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="44222-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="44222-216">In Hallo **actie** sectie staan alle Hallo toegestane bewerkingen voor deze rol.</span><span class="sxs-lookup"><span data-stu-id="44222-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="44222-217">Het is belangrijk toounderstand dat elke actie van een resourceprovider is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="44222-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="44222-218">In dit geval voor het maken van ondersteuning tickets Hallo **Microsoft.Support** resourceprovider moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="44222-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="44222-219">toobe kunnen toosee alle Hallo resourceproviders beschikbaar is en geregistreerd in uw abonnement, kunt u PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44222-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="44222-220">Bovendien kunt u controleren voor Hallo alle Hallo beschikbaar PowerShell-cmdlets toomanage hello resourceproviders.</span><span class="sxs-lookup"><span data-stu-id="44222-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="44222-221">![Schermopname van PowerShell voor provider bronbeheer](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="44222-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="44222-222">alle acties voor een bepaalde RBAC-rol, resource providers worden vermeld in de sectie Hallo Hallo toorestrict **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="44222-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="44222-223">Laatste, is het verplichte dat die Hallo RBAC-rol bevat Hallo expliciete abonnement-id's waar het wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44222-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="44222-224">Hallo abonnement-id's vermeld onder Hallo **AssignableScopes**, anders u pas weer toegestaan tooimport Hallo rol in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="44222-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="44222-225">Na het maken en aanpassen van Hallo RBAC-rol, moet deze toobe geïmporteerde back Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="44222-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="44222-226">In dit voorbeeld is aangepaste naam voor deze rol RBAC Hallo 'Lezer ondersteuning tickets toegangsniveau' hello gebruiker tooview alles zodat in Hallo-abonnement en ook tooopen ondersteuningsaanvragen.</span><span class="sxs-lookup"><span data-stu-id="44222-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="44222-227">Hallo slechts twee ingebouwde RBAC-rollen zodat Hallo actie van het openen van ondersteuningsaanvragen zijn **eigenaar** en **Inzender**.</span><span class="sxs-lookup"><span data-stu-id="44222-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="44222-228">Voor een gebruiker toobe kunnen tooopen ondersteuningsaanvragen, moet hij worden toegewezen een RBAC-rol alleen op Hallo abonnementsbereik, omdat alle ondersteuningsaanvragen zijn gemaakt op basis van een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="44222-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="44222-229">Deze nieuwe aangepaste rol is toegewezen tooan gebruiker Hallo dezelfde directory.</span><span class="sxs-lookup"><span data-stu-id="44222-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![schermopname van aangepaste RBAC-rol in Hallo geïmporteerd met Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![schermopname van het toewijzen van aangepaste geïmporteerde RBAC-rol toouser in Hallo dezelfde directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![schermopname van machtigingen voor aangepaste geïmporteerde RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="44222-233">Hallo-voorbeeld is meer gedetailleerde tooemphasize Hallo limieten van deze aangepaste RBAC-rol als volgt:</span><span class="sxs-lookup"><span data-stu-id="44222-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="44222-234">Nieuwe ondersteuningsaanvragen kunt maken</span><span class="sxs-lookup"><span data-stu-id="44222-234">Can create new support requests</span></span>
* <span data-ttu-id="44222-235">Nieuwe scopes van de resource kan niet worden gemaakt (bijvoorbeeld: virtuele machine)</span><span class="sxs-lookup"><span data-stu-id="44222-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="44222-236">Kan de nieuwe resourcegroepen niet maken.</span><span class="sxs-lookup"><span data-stu-id="44222-236">Can't create new resource groups</span></span>





![schermopname van aangepaste RBAC-rol ondersteuningsaanvragen maken](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![schermopname van aangepaste RBAC-rol kan niet toocreate virtuele machines](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![schermopname van aangepaste RBAC-rol kan niet toocreate nieuwe RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="44222-240">Maak een aangepaste RBAC-rol tooopen ondersteuning-aanvragen via de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="44222-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="44222-241">Uitgevoerd op een Mac en zonder toegang tooPowerShell, is Azure CLI Hallo manier toogo.</span><span class="sxs-lookup"><span data-stu-id="44222-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="44222-242">Hallo stappen toocreate een aangepaste beveiligingsrol zijn Hallo dezelfde zijn, met de enige uitzondering Hallo dat met CLI Hallo-rol kan niet worden gedownload in een JSON-sjabloon, maar kan worden bekeken in Hallo CLI.</span><span class="sxs-lookup"><span data-stu-id="44222-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="44222-243">Voor dit voorbeeld ik hebt gekozen, is een ingebouwde rol Hallo van **back-up lezer**.</span><span class="sxs-lookup"><span data-stu-id="44222-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Schermafbeelding van de rol van back-lezer CLI weergeven](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="44222-245">Hallo-rol in Visual Studio na het kopiëren van Hallo eigenschappen in een JSON-sjabloon bewerkt, Hallo **Microsoft.Support** resourceprovider is toegevoegd aan Hallo **acties** secties zodat deze gebruiker kunt openen ondersteuningsaanvragen terwijl u een lezer voor de back-upkluizen hello toobe.</span><span class="sxs-lookup"><span data-stu-id="44222-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="44222-246">Opnieuw verdient het benodigde tooadd Hallo abonnements-ID waar deze rol wordt gebruikt in Hallo **AssignableScopes** sectie.</span><span class="sxs-lookup"><span data-stu-id="44222-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![CLI-schermopname van het importeren van aangepaste RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="44222-248">de nieuwe rol Hallo is nu beschikbaar in hello Azure-portal en Hallo toewijzing proces is dezelfde als in de eerdere voorbeelden Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44222-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Azure portal schermafbeelding van aangepaste RBAC-rol gemaakt met behulp van de CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="44222-250">Op Hallo is de meest recente Build 2017 hello Azure Cloud Shell algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="44222-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="44222-251">Azure Cloud-Shell is een aanvulling tooIDE en hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="44222-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="44222-252">Met deze service krijgt u een browser gebaseerde shell die is geverifieerd en wordt gehost in Azure en u kunt deze gebruiken in plaats van de CLI op uw computer geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="44222-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure-Cloud-Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
