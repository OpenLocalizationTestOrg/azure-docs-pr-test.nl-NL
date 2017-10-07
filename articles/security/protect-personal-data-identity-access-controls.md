---
title: persoonlijke gegevens met Azure identiteits- en toegangsbeheer besturingselementen aaaProtect | Microsoft Docs
description: Met behulp van Azure identiteits- en toegangsbeheer besturingselementen toohelp beveiligen u uw persoonlijke gegevens
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="45b9d-103">Azure Active Directory en de multi-factor Authentication: persoonlijke gegevens beschermen met besturingselementen voor identiteits- en toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="45b9d-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="45b9d-104">Dit artikel bevat informatie en procedures kunt u tooprotect persoonlijke gegevens met behulp van Azure Active Directory en de multi-factor authentication-beveiligingsfuncties en -services.</span><span class="sxs-lookup"><span data-stu-id="45b9d-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="45b9d-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="45b9d-105">Scenario</span></span>

<span data-ttu-id="45b9d-106">Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="45b9d-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="45b9d-107">toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, verkregen Duitsland, Denemarken en Hallo Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="45b9d-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="45b9d-108">Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="45b9d-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="45b9d-109">Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase.</span><span class="sxs-lookup"><span data-stu-id="45b9d-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="45b9d-110">Dit omvat ook traditionele Human Resources informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties.</span><span class="sxs-lookup"><span data-stu-id="45b9d-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="45b9d-111">Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.</span><span class="sxs-lookup"><span data-stu-id="45b9d-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="45b9d-112">Zakelijke werknemers toegang tot het Hallo netwerk van de externe kantoren en reizen agents van het bedrijf Hallo wereld Hallo zich toegang tot toosome bedrijfsbronnen hebben.</span><span class="sxs-lookup"><span data-stu-id="45b9d-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="45b9d-113">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="45b9d-113">Problem statement</span></span>

<span data-ttu-id="45b9d-114">Hallo bedrijf moet Hallo privacy van klanten en werknemers persoonlijke gegevens beveiligen tegen kwaadwillende personen toouse geknoeid identiteiten toogain toegang zoeken.</span><span class="sxs-lookup"><span data-stu-id="45b9d-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="45b9d-115">Ze ook moeten ervoor zorgen dat toegang toopersonal gegevens door legitieme gebruikers is beperkt tot alleen degenen die u nodig hebt toodo hun werk.</span><span class="sxs-lookup"><span data-stu-id="45b9d-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="45b9d-116">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="45b9d-116">Company goal</span></span>

<span data-ttu-id="45b9d-117">doel van het bedrijf Hallo is tooensure die toegang tot gegevens toopersonal strikt worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="45b9d-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="45b9d-118">Het is essentieel dat de identiteit van gebruikers met toegang tot toopersonal gegevens door sterke verificatie worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="45b9d-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="45b9d-119">Een beleid van [minimale bevoegdheden] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) moeten worden afgedwongen, zodat legitieme gebruikers hoeven alleen Hallo niveau van toegang hebben en niet meer.</span><span class="sxs-lookup"><span data-stu-id="45b9d-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="45b9d-120">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="45b9d-120">Solutions</span></span>

<span data-ttu-id="45b9d-121">Microsoft Azure biedt beheerprogramma's voor identiteits- en toegangsbeheer toohelp bedrijven bepalen wie heeft toegang tot tooresources die persoonlijke gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="45b9d-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="45b9d-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45b9d-122">Azure Active Directory</span></span>

<span data-ttu-id="45b9d-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) beheert identiteiten en beheert de toegang tooAzure evenals andere on-premises en andere cloudbronnen, gegevens en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="45b9d-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="45b9d-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helpt Azure beheerders toominimize Hallo aantal mensen toegang toocertain informatie zoals persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="45b9d-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="45b9d-125">Deze manier kunnen toodiscover, Beperk en bewaak bevoegde identiteiten en hun access tooresources en tooassign tijdelijke, JIT (Just in time) beheerdersrechten tooeligible-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45b9d-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="45b9d-126">Het bevat ook inzicht in de AAD-beheerdersbevoegdheden hebben.</span><span class="sxs-lookup"><span data-stu-id="45b9d-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="45b9d-127">Hallo-activiteiten die betrokken zijn bij het gebruik van AAD PIM omvatten:</span><span class="sxs-lookup"><span data-stu-id="45b9d-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="45b9d-128">Privileged Identity Management voor uw directory inschakelen</span><span class="sxs-lookup"><span data-stu-id="45b9d-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="45b9d-129">Met behulp van Privileged Identity Management admin dashboard toosee belangrijke informatie in een oogopslag</span><span class="sxs-lookup"><span data-stu-id="45b9d-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="45b9d-130">Hallo bevoegde identiteiten (beheerders) toe te voegen of te verwijderen of de in aanmerking komende beheerders tooeach functie beheren</span><span class="sxs-lookup"><span data-stu-id="45b9d-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="45b9d-131">Hallo rol activeringsinstellingen configureren</span><span class="sxs-lookup"><span data-stu-id="45b9d-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="45b9d-132">Rollen activeren</span><span class="sxs-lookup"><span data-stu-id="45b9d-132">Activating roles</span></span>

- <span data-ttu-id="45b9d-133">Rol activiteit controleren</span><span class="sxs-lookup"><span data-stu-id="45b9d-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="45b9d-134">Hoe kan ik AAD PIM inschakelen?</span><span class="sxs-lookup"><span data-stu-id="45b9d-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="45b9d-135">met behulp van PIM voor uw directory toostart Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="45b9d-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="45b9d-136">Meld u toohello Azure-portal als globale beheerder van uw directory.</span><span class="sxs-lookup"><span data-stu-id="45b9d-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="45b9d-137">Als uw organisatie meer dan één map heeft, selecteert u uw gebruikersnaam in Hallo rechterbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="45b9d-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="45b9d-138">Selecteer Hallo map waar u Azure AD Privileged Identity Management gebruikt.</span><span class="sxs-lookup"><span data-stu-id="45b9d-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="45b9d-139">Selecteer **meer services** en gebruik Hallo **Filter** textbox toosearch voor Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="45b9d-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="45b9d-140">Controleer **pincode toodashboard** en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="45b9d-141">Hallo Privileged Identity Management-toepassing wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="45b9d-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="45b9d-142">Nadat Azure AD Privileged Identity Management is ingesteld, ziet u Hallo navigatie blade wanneer u de toepassing hello opent.</span><span class="sxs-lookup"><span data-stu-id="45b9d-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="45b9d-143">Zie voor meer informatie en instructies voor het aan de slag met AAD PIM [Start met behulp van Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="45b9d-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="45b9d-144">Op rollen gebaseerde toegangsbeheer van Azure</span><span class="sxs-lookup"><span data-stu-id="45b9d-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="45b9d-145">[Azure op rollen gebaseerd toegangsbeheer](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helpt Azure access tooAzure bronnen beheren door in te schakelen Hallo verlenen van toegang op basis van de toegewezen rol van de gebruiker van het Hallo-beheerders.</span><span class="sxs-lookup"><span data-stu-id="45b9d-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="45b9d-146">U kunt taken in een team scheiden en verleen alleen Hallo hoeveelheid toegang toousers, groepen en toepassingen die zij nodig hebben tooperform hun werk.</span><span class="sxs-lookup"><span data-stu-id="45b9d-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="45b9d-147">Op rollen gebaseerde toegang kan worden verleend als toousers met hello Azure-portal, Azure-opdrachtregelprogramma's of Azure Management-API's.</span><span class="sxs-lookup"><span data-stu-id="45b9d-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="45b9d-148">Zie voor meer informatie over de basisprincipes van Azure RBAC [aan de slag met toegangsbeheer op basis van rollen in hello Azure-Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="45b9d-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="45b9d-149">Hoe beheer ik Azure RBAC met PowerShell</span><span class="sxs-lookup"><span data-stu-id="45b9d-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="45b9d-150">U kunt de PowerShell-cmdlets toomanage Azure RBAC, met inbegrip van de volgende beheertaken Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="45b9d-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="45b9d-151">Lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="45b9d-151">List roles</span></span>

- <span data-ttu-id="45b9d-152">Zien wie toegang heeft</span><span class="sxs-lookup"><span data-stu-id="45b9d-152">See who has access</span></span>

- <span data-ttu-id="45b9d-153">Toegang verlenen</span><span class="sxs-lookup"><span data-stu-id="45b9d-153">Grant access</span></span>

- <span data-ttu-id="45b9d-154">Toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="45b9d-154">Remove access</span></span>

- <span data-ttu-id="45b9d-155">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="45b9d-155">Create a custom role</span></span>

- <span data-ttu-id="45b9d-156">Acties voor een Resourceprovider ophalen</span><span class="sxs-lookup"><span data-stu-id="45b9d-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="45b9d-157">Een aangepaste rol wijzigen</span><span class="sxs-lookup"><span data-stu-id="45b9d-157">Modify a custom role</span></span>

- <span data-ttu-id="45b9d-158">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="45b9d-158">Delete a custom role</span></span>

- <span data-ttu-id="45b9d-159">Lijst met aangepaste rollen</span><span class="sxs-lookup"><span data-stu-id="45b9d-159">List custom roles</span></span>

<span data-ttu-id="45b9d-160">Voor instructies over hoe toomanage Azure RBAC met PowerShell, Zie [toegang op basis van rollen beheren met Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="45b9d-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="45b9d-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="45b9d-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="45b9d-162">[Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is een verificatie-oplossing voor in twee stappen waarmee beveiliging toegang toodata en toepassingen, en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="45b9d-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="45b9d-163">Het biedt krachtige verificatie via een reeks verificatiemethoden waaronder verificatie per telefoon, sms of mobiele app.</span><span class="sxs-lookup"><span data-stu-id="45b9d-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="45b9d-164">toodeploy MFA in hello Azure-cloud, moet u toofirst inschakelen en schakelt u verificatie in twee stappen voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="45b9d-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="45b9d-165">Hoe kan ik Azure toouse MFA inschakelen?</span><span class="sxs-lookup"><span data-stu-id="45b9d-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="45b9d-166">Als uw gebruikers licenties met Azure multi-factor Authentication hebt, is er niets hoeft toodo tooturn op Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="45b9d-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="45b9d-167">Als dat niet het geval is, moet u een multi-factor Authentication-provider toocreate in uw directory.</span><span class="sxs-lookup"><span data-stu-id="45b9d-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="45b9d-168">toodo dit als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="45b9d-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="45b9d-169">Selecteer **Active Directory** in Hallo klassieke Azure-portal (aangemeld als beheerder).</span><span class="sxs-lookup"><span data-stu-id="45b9d-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="45b9d-170">Selecteer **multi-factor Authentication-Providers.**</span><span class="sxs-lookup"><span data-stu-id="45b9d-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="45b9d-171">Selecteer **nieuw** en klik vervolgens onder **App-Services,** Selecteer **multi-factor Authentication-Provider.**</span><span class="sxs-lookup"><span data-stu-id="45b9d-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="45b9d-172">Selecteer **snelle invoer.**</span><span class="sxs-lookup"><span data-stu-id="45b9d-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="45b9d-173">Vul in het naamveld Hallo en selecteer een gebruiksmodel (per authenticatie of per ingeschakelde gebruiker).</span><span class="sxs-lookup"><span data-stu-id="45b9d-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="45b9d-174">Wijst een map aan welke Hallo MFA-Provider gekoppeld is.</span><span class="sxs-lookup"><span data-stu-id="45b9d-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="45b9d-175">Klik op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="45b9d-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="45b9d-176">Voor meer instructies voor het toomanage uw multi-factor Authentication-Provider Zie [aan de slag met een Azure multi-factor Authentication-Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="45b9d-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="45b9d-177">Hoe schakel ik verificatie in twee stappen voor gebruikers?</span><span class="sxs-lookup"><span data-stu-id="45b9d-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="45b9d-178">U kunt de verificatie in twee stappen voor alle aanmeldingen afdwingen of kunt u verificatie van voorwaardelijk beleid toorequire in twee stappen alleen wanneer bepaalde voorwaarden van toepassing.</span><span class="sxs-lookup"><span data-stu-id="45b9d-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="45b9d-179">Azure MFA inschakelen door het wijzigen van de status van gebruikers is Hallo traditionele aanpak voor het vereisen van verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="45b9d-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="45b9d-180">Alle Hallo-gebruikers die u inschakelt, hebben dezelfde verificatie van vereiste tooperform in twee stappen Hallo telkens wanneer ze zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="45b9d-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="45b9d-181">Alle beleidsregels voor voorwaardelijke toegang die mogelijk gevolgen hebben voor die gebruiker inschakelen van een gebruiker worden onderdrukt.</span><span class="sxs-lookup"><span data-stu-id="45b9d-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="45b9d-182">Azure MFA inschakelen met een beleid voor voorwaardelijke toegang is een flexibelere benadering voor het vereisen van verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="45b9d-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="45b9d-183">U kunt beleid voor voorwaardelijke toegang die van toepassing toogroups zoals afzonderlijke gebruikers maken.</span><span class="sxs-lookup"><span data-stu-id="45b9d-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="45b9d-184">Met een hoog risico groepen meer beperkingen dan laag risico groepen kunnen worden opgegeven of verificatie in twee stappen kan worden alleen vereist voor met een hoog risico cloud-apps en voor de laag risico die zijn overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="45b9d-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="45b9d-185">Voorwaardelijke toegang is echter een betaald functie van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="45b9d-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="45b9d-186">tooenable MFA door het wijzigen van de status van de gebruiker, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="45b9d-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="45b9d-187">Meld u toohello Azure-portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="45b9d-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="45b9d-188">Ga te**Azure Active Directory \> gebruikers en groepen \> alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="45b9d-189">Selecteer **multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="45b9d-190">Zoeken naar Hallo gebruiker gewenste tooenable voor Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="45b9d-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="45b9d-191">Mogelijk moet u toochange weergave boven Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="45b9d-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="45b9d-192">Controleer de naam van de Hallo vak volgende toohello van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="45b9d-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="45b9d-193">Kies op Hallo rechts en onder snelle stappen, **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="45b9d-194">Bevestig uw selectie in Hallo pop-upvenster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="45b9d-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="45b9d-195">Gebruikers voor wie MFA is ingeschakeld wordt gevraagd tooregister Hallo wanneer die ze zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="45b9d-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="45b9d-196">tooenable Azure MFA met beleid voor voorwaardelijke toegang, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="45b9d-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="45b9d-197">Meld u toohello Azure-portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="45b9d-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="45b9d-198">Ga te**Azure Active Directory \> voorwaardelijke toegang**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="45b9d-199">Selecteer **nieuw beleid**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-199">Select **New policy**.</span></span>

4. <span data-ttu-id="45b9d-200">Onder **toewijzingen**, selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="45b9d-201">Gebruik Hallo **opnemen** en **uitsluiten** toospecify welke gebruikers en groepen worden beheerd door beleid Hallo tabbladen.</span><span class="sxs-lookup"><span data-stu-id="45b9d-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="45b9d-202">Onder **toewijzingen**, selecteer **Cloud-apps.**</span><span class="sxs-lookup"><span data-stu-id="45b9d-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="45b9d-203">Kies te**omvatten alle cloud-apps**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="45b9d-204">Onder **toegangscontroles**, selecteer **Grant**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="45b9d-205">Kies **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="45b9d-206">Schakel **beleid inschakelen** te**op** en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="45b9d-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="45b9d-207">Voor informatie over hoe tooconfigure Azure MFA-instellingen tooset van Fraudewaarschuwingen, maakt een eenmalig overslaan, aangepaste spraakberichten gebruiken, caching configureren, goedgekeurde IP-adressen opgeven, app-wachtwoorden maken, onthoud MFA voor apparaten die gebruikers vertrouwt, en selecteer inschakelen verificatiemethoden, Zie [Azure multi-factor Authentication-instellingen configureren.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="45b9d-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="45b9d-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45b9d-208">Next steps</span></span>

- [<span data-ttu-id="45b9d-209">Bevoegde toegang beveiligen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="45b9d-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="45b9d-210">Veelgestelde vragen over Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="45b9d-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="45b9d-211">Probleemoplossing voor toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="45b9d-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="45b9d-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="45b9d-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
