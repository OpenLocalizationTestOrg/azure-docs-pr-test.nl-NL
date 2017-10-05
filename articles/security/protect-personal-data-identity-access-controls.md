---
title: Persoonlijke gegevens beschermen met Azure identiteits- en toegangsbeheer besturingselementen | Microsoft Docs
description: Met behulp van Azure identiteits- en toegangsbeheer bepaalt voor hulp bij het beveiligen van uw persoonlijke gegevens
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
ms.openlocfilehash: b43754efd207679dbe08710f44f56454a5fd20ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="48188-103">Azure Active Directory en de multi-factor Authentication: persoonlijke gegevens beschermen met besturingselementen voor identiteits- en toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="48188-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="48188-104">Dit artikel bevat informatie en procedures die u gebruiken kunt voor het beveiligen van persoonlijke gegevens met Azure Active Directory en de multi-factor authentication-beveiligingsfuncties en -services.</span><span class="sxs-lookup"><span data-stu-id="48188-104">This article provides information and procedures you can use to protect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="48188-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="48188-105">Scenario</span></span>

<span data-ttu-id="48188-106">Een bedrijf grote cruise, gevestigd in de Verenigde Staten, aanvullende bewerkingen voor het bieden van routes in de Middellandse, Adriatische, Baltische veiligheid ook Florida.</span><span class="sxs-lookup"><span data-stu-id="48188-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="48188-107">Ter ondersteuning van deze inspanningen is die is verkregen meerdere kleinere cruise regels op basis van Italië, Duitsland, Denemarken en het Verenigd Koninkrijk</span><span class="sxs-lookup"><span data-stu-id="48188-107">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="48188-108">Het bedrijf gebruikmaakt van Microsoft Azure voor het opslaan van bedrijfsgegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="48188-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="48188-109">Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase.</span><span class="sxs-lookup"><span data-stu-id="48188-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="48188-110">Dit omvat ook traditionele Human Resources informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties.</span><span class="sxs-lookup"><span data-stu-id="48188-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="48188-111">De regel cruise onderhoudt ook een grote database van derden en loyaliteit programma leden met persoonlijke gegevens voor de relaties met de huidige en eerdere klanten bijhouden.</span><span class="sxs-lookup"><span data-stu-id="48188-111">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="48188-112">Zakelijke werknemers toegang tot het netwerk van het bedrijf externe kantoren en reizen agents over de hele wereld hebben toegang tot een aantal bedrijfsresources.</span><span class="sxs-lookup"><span data-stu-id="48188-112">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="48188-113">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="48188-113">Problem statement</span></span>

<span data-ttu-id="48188-114">Het bedrijf moet de privacy van klanten en werknemers persoonlijke gegevens beveiligen tegen kwaadwillende personen willen waarmee is geknoeid id's gebruiken om toegang te krijgen.</span><span class="sxs-lookup"><span data-stu-id="48188-114">The company must protect the privacy of customers’ and employees’ personal data from attackers seeking to use compromised identities to gain access.</span></span> <span data-ttu-id="48188-115">Ze ook moeten ervoor zorgen dat de toegang tot persoonlijke gegevens door legitieme gebruikers is beperkt tot alleen degenen die u nodig hebt om hun werk te doen.</span><span class="sxs-lookup"><span data-stu-id="48188-115">They also must ensure that access to personal data by legitimate users is restricted to only those who need it to do their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="48188-116">Bedrijf-doel</span><span class="sxs-lookup"><span data-stu-id="48188-116">Company goal</span></span>

<span data-ttu-id="48188-117">Doel van het bedrijf is om ervoor te zorgen dat toegang tot persoonlijke gegevens strikt wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="48188-117">The company’s goal is to ensure that access to personal data is strictly controlled.</span></span> <span data-ttu-id="48188-118">Het is essentieel dat de identiteit van gebruikers met toegang tot persoonlijke gegevens door sterke verificatie worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="48188-118">It is essential that identities of users with access to personal data be protected by strong authentication.</span></span> <span data-ttu-id="48188-119">Een beleid van [minimale bevoegdheden] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) moeten worden afgedwongen, zodat legitieme gebruikers hoeven alleen het niveau van toegang hebben en niet meer.</span><span class="sxs-lookup"><span data-stu-id="48188-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only the level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="48188-120">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="48188-120">Solutions</span></span>

<span data-ttu-id="48188-121">Microsoft Azure biedt identiteits- en toegangsbeheer beheerhulpprogramma's, zodat bedrijven bepalen wie toegang heeft tot bronnen die persoonlijke gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="48188-121">Microsoft Azure provides identity and access management tools to help companies control who has access to resources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="48188-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48188-122">Azure Active Directory</span></span>

<span data-ttu-id="48188-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) beheert identiteiten en controleert de toegang tot Azure evenals andere on-premises en andere cloudbronnen, gegevens en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="48188-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access to Azure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="48188-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) bedoeld om beheerders van Azure om het aantal mensen die toegang tot bepaalde gegevens zoals persoonlijke gegevens hebben te beperken.</span><span class="sxs-lookup"><span data-stu-id="48188-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators to minimize the number of people who have access to certain information such as personal data.</span></span> <span data-ttu-id="48188-125">Dit kan ze detecteren, te beperken en te controleren van bevoegde identiteiten en de toegang tot bronnen en toe te wijzen tijdelijke, beheerdersrechten hebben voor gebruikers in aanmerking komende JIT (Just in time).</span><span class="sxs-lookup"><span data-stu-id="48188-125">It enables them to discover, restrict, and monitor privileged identities and their access to resources, and to assign temporary, Just-In-Time (JIT) administrative rights to eligible users.</span></span> <span data-ttu-id="48188-126">Het bevat ook inzicht in de AAD-beheerdersbevoegdheden hebben.</span><span class="sxs-lookup"><span data-stu-id="48188-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="48188-127">De activiteiten die betrokken zijn bij het gebruik van AAD PIM omvatten:</span><span class="sxs-lookup"><span data-stu-id="48188-127">The activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="48188-128">Privileged Identity Management voor uw directory inschakelen</span><span class="sxs-lookup"><span data-stu-id="48188-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="48188-129">Met behulp van Privileged Identity Management admin dashboard belangrijke informatie in één oogopslag zien</span><span class="sxs-lookup"><span data-stu-id="48188-129">Using Privileged Identity Management admin dashboard to see important information at a glance</span></span>

- <span data-ttu-id="48188-130">Het beheren van de bevoegde identiteiten (beheerders) toe te voegen of te verwijderen of de in aanmerking komende beheerders aan elke rol</span><span class="sxs-lookup"><span data-stu-id="48188-130">Managing the privileged identities (administrators) by adding or removing permanent or eligible administrators to each role</span></span>

- <span data-ttu-id="48188-131">De instellingen van de activering configureren</span><span class="sxs-lookup"><span data-stu-id="48188-131">Configuring the role activation settings</span></span>

- <span data-ttu-id="48188-132">Rollen activeren</span><span class="sxs-lookup"><span data-stu-id="48188-132">Activating roles</span></span>

- <span data-ttu-id="48188-133">Rol activiteit controleren</span><span class="sxs-lookup"><span data-stu-id="48188-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="48188-134">Hoe kan ik AAD PIM inschakelen?</span><span class="sxs-lookup"><span data-stu-id="48188-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="48188-135">Als u wilt gebruiken PIM voor uw directory, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="48188-135">To start using PIM for your directory, do the following:</span></span>

1. <span data-ttu-id="48188-136">Meld u aan bij de Azure portal als globale beheerder van uw directory.</span><span class="sxs-lookup"><span data-stu-id="48188-136">Sign in to the Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="48188-137">Als uw organisatie meerdere directory's heeft, selecteert u uw gebruikersnaam rechtsboven in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="48188-137">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="48188-138">Selecteer de map waar u Azure AD Privileged Identity Management gebruikt.</span><span class="sxs-lookup"><span data-stu-id="48188-138">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="48188-139">Selecteer **meer services** en gebruik de **Filter** textbox om te zoeken naar Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="48188-139">Select **More services** and use the **Filter** textbox to search for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="48188-140">Schakel **Vastmaken aan dashboard** in en klik op de knop **Maken**.</span><span class="sxs-lookup"><span data-stu-id="48188-140">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="48188-141">De Privileged Identity Management-toepassing wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="48188-141">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="48188-142">Nadat Azure AD Privileged Identity Management is ingesteld, ziet u de navigatieblade telkens wanneer u de toepassing opent.</span><span class="sxs-lookup"><span data-stu-id="48188-142">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="48188-143">Zie voor meer informatie en instructies voor het aan de slag met AAD PIM [Start met behulp van Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="48188-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="48188-144">Op rollen gebaseerde toegangsbeheer van Azure</span><span class="sxs-lookup"><span data-stu-id="48188-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="48188-145">[Azure op rollen gebaseerd toegangsbeheer](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helpt Azure beheerders toegang tot Azure-resources beheren doordat het verlenen van toegang op basis van de gebruiker toegewezen rol.</span><span class="sxs-lookup"><span data-stu-id="48188-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access to Azure resources by enabling the granting of access based on the user’s assigned role.</span></span> <span data-ttu-id="48188-146">U kunt taken in een team scheiden en de hoeveelheid toegang verlenen aan gebruikers, groepen en toepassingen die ze nodig hebben voor het uitvoeren van hun taken.</span><span class="sxs-lookup"><span data-stu-id="48188-146">You can segregate duties within a team and grant only the amount of access to users, groups and applications that they need to perform their jobs.</span></span>

<span data-ttu-id="48188-147">Op rollen gebaseerde toegang kan worden verleend aan gebruikers via de Azure Portal, Azure-opdrachtregelprogramma's of Azure Management-API's.</span><span class="sxs-lookup"><span data-stu-id="48188-147">Role-based access can be granted to users using the Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="48188-148">Zie voor meer informatie over de basisprincipes van Azure RBAC [aan de slag met toegangsbeheer op basis van rollen in Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="48188-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in the Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="48188-149">Hoe beheer ik Azure RBAC met PowerShell</span><span class="sxs-lookup"><span data-stu-id="48188-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="48188-150">U kunt de PowerShell-cmdlets gebruiken voor het beheren van Azure RBAC, met inbegrip van de volgende beheertaken:</span><span class="sxs-lookup"><span data-stu-id="48188-150">You can use PowerShell cmdlets to manage Azure RBAC, including the following management tasks:</span></span>

- <span data-ttu-id="48188-151">Lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="48188-151">List roles</span></span>

- <span data-ttu-id="48188-152">Zien wie toegang heeft</span><span class="sxs-lookup"><span data-stu-id="48188-152">See who has access</span></span>

- <span data-ttu-id="48188-153">Toegang verlenen</span><span class="sxs-lookup"><span data-stu-id="48188-153">Grant access</span></span>

- <span data-ttu-id="48188-154">Toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="48188-154">Remove access</span></span>

- <span data-ttu-id="48188-155">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="48188-155">Create a custom role</span></span>

- <span data-ttu-id="48188-156">Acties voor een Resourceprovider ophalen</span><span class="sxs-lookup"><span data-stu-id="48188-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="48188-157">Een aangepaste rol wijzigen</span><span class="sxs-lookup"><span data-stu-id="48188-157">Modify a custom role</span></span>

- <span data-ttu-id="48188-158">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="48188-158">Delete a custom role</span></span>

- <span data-ttu-id="48188-159">Lijst met aangepaste rollen</span><span class="sxs-lookup"><span data-stu-id="48188-159">List custom roles</span></span>

<span data-ttu-id="48188-160">Zie voor instructies over het beheren van Azure RBAC met PowerShell [toegang op basis van rollen beheren met Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="48188-160">For instructions on how to manage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="48188-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="48188-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="48188-162">[Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is een in twee stappen verificatie-oplossing waarmee u toegang tot gegevens en toepassingen, beveiligt en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden.</span><span class="sxs-lookup"><span data-stu-id="48188-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access to data and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="48188-163">Het biedt krachtige verificatie via een reeks verificatiemethoden waaronder verificatie per telefoon, sms of mobiele app.</span><span class="sxs-lookup"><span data-stu-id="48188-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="48188-164">Voor het implementeren van MFA in de Azure-cloud, moet u deze eerst inschakelen en schakelt u verificatie in twee stappen voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="48188-164">To deploy MFA in the Azure cloud, you need to first enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-to-use-mfa"></a><span data-ttu-id="48188-165">Hoe schakel ik Azure MFA gebruiken?</span><span class="sxs-lookup"><span data-stu-id="48188-165">How do I enable Azure to use MFA?</span></span>

<span data-ttu-id="48188-166">Als uw gebruikers licenties met Azure multi-factor Authentication hebt, is er niets die u moet doen om de Azure MFA inschakelen.</span><span class="sxs-lookup"><span data-stu-id="48188-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="48188-167">Als dat niet het geval is, moet u een multi-factor Authentication-provider maken in uw directory.</span><span class="sxs-lookup"><span data-stu-id="48188-167">If not, you need to create a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="48188-168">U doet dit door de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="48188-168">To do this, follow these steps:</span></span>

1. <span data-ttu-id="48188-169">Selecteer **Active Directory** in de klassieke Azure portal (aangemeld als beheerder).</span><span class="sxs-lookup"><span data-stu-id="48188-169">Select **Active Directory** in the Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="48188-170">Selecteer **multi-factor Authentication-Providers.**</span><span class="sxs-lookup"><span data-stu-id="48188-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="48188-171">Selecteer **nieuw** en klik vervolgens onder **App-Services,** Selecteer **multi-factor Authentication-Provider.**</span><span class="sxs-lookup"><span data-stu-id="48188-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="48188-172">Selecteer **snelle invoer.**</span><span class="sxs-lookup"><span data-stu-id="48188-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="48188-173">Vul het naamveld in en selecteer een gebruiksmodel (per authenticatie of per ingeschakelde gebruiker).</span><span class="sxs-lookup"><span data-stu-id="48188-173">Fill in the name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="48188-174">Wijst een map waar de MFA-Provider gekoppeld wordt.</span><span class="sxs-lookup"><span data-stu-id="48188-174">Designate a directory with which the MFA Provider is associated.</span></span>

7. <span data-ttu-id="48188-175">Klik op de knop **Maken**.</span><span class="sxs-lookup"><span data-stu-id="48188-175">Click the **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="48188-176">Zie voor meer instructies voor het beheren van uw multi-factor Authentication-Provider [aan de slag met een Azure multi-factor Authentication-Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="48188-176">For more instructions on how to manage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="48188-177">Hoe schakel ik verificatie in twee stappen voor gebruikers?</span><span class="sxs-lookup"><span data-stu-id="48188-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="48188-178">U kunt afdwingen dat de verificatie in twee stappen voor alle aanmeldingen of kunt u beleidsregels voor voorwaardelijke toegang om te vereisen verificatie in twee stappen alleen wanneer bepaalde voorwaarden van toepassing.</span><span class="sxs-lookup"><span data-stu-id="48188-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="48188-179">Azure MFA inschakelen door het wijzigen van de status van gebruikers is de traditionele aanpak voor het vereisen van verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="48188-179">Enabling Azure MFA by changing user states is the traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="48188-180">Verificatie in twee stappen uitvoeren telkens wanneer ze zich dezelfde vereisten hebben alle gebruikers die u inschakelt.</span><span class="sxs-lookup"><span data-stu-id="48188-180">All the users that you enable will have the same requirement to perform two-step verification every time they sign in.</span></span> <span data-ttu-id="48188-181">Alle beleidsregels voor voorwaardelijke toegang die mogelijk gevolgen hebben voor die gebruiker inschakelen van een gebruiker worden onderdrukt.</span><span class="sxs-lookup"><span data-stu-id="48188-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="48188-182">Azure MFA inschakelen met een beleid voor voorwaardelijke toegang is een flexibelere benadering voor het vereisen van verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="48188-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="48188-183">U kunt beleid voor voorwaardelijke toegang die voor zowel afzonderlijke gebruikers als groepen gelden maken.</span><span class="sxs-lookup"><span data-stu-id="48188-183">You can create conditional access policies that apply to groups as well as individual users.</span></span> <span data-ttu-id="48188-184">Met een hoog risico groepen meer beperkingen dan laag risico groepen kunnen worden opgegeven of verificatie in twee stappen kan worden alleen vereist voor met een hoog risico cloud-apps en voor de laag risico die zijn overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="48188-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="48188-185">Voorwaardelijke toegang is echter een betaald functie van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48188-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="48188-186">Schakel MFA door het wijzigen van de status van gebruiker door het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="48188-186">To enable MFA by changing user state, do the following:</span></span>

1. <span data-ttu-id="48188-187">Meld u aan bij de Azure portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="48188-187">Sign in to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="48188-188">Ga naar **Azure Active Directory \> gebruikers en groepen \> alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="48188-188">Go to **Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="48188-189">Selecteer **multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="48188-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="48188-190">Zoek de gebruiker die u wilt inschakelen voor Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="48188-190">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="48188-191">Mogelijk moet u de weergave bovenaan wijzigen.</span><span class="sxs-lookup"><span data-stu-id="48188-191">You may need to change the view at the top.</span></span>
5. <span data-ttu-id="48188-192">Schakel het selectievakje naast de naam van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="48188-192">Check the box next to the user’s name.</span></span>
6. <span data-ttu-id="48188-193">Kies aan de rechterkant, onder snelle stappen **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="48188-193">On the right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="48188-194">Bevestig uw selectie in het pop-upvenster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="48188-194">Confirm your selection in the pop-up window that opens.</span></span>  <span data-ttu-id="48188-195">Gebruikers voor wie MFA is ingeschakeld wordt gevraagd om te registreren van de volgende keer dat ze zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="48188-195">Users for whom MFA has been enabled will be asked to register the next time they sign in.</span></span>

<span data-ttu-id="48188-196">Schakel Azure MFA met beleid voor voorwaardelijke toegang door het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="48188-196">To enable Azure MFA with a conditional access policy, do the following:</span></span>

1. <span data-ttu-id="48188-197">Meld u aan bij de Azure portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="48188-197">Sign in to the Azure portal as an administrator.</span></span>

2. <span data-ttu-id="48188-198">Ga naar **Azure Active Directory \> voorwaardelijke toegang**.</span><span class="sxs-lookup"><span data-stu-id="48188-198">Go to **Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="48188-199">Selecteer **nieuw beleid**.</span><span class="sxs-lookup"><span data-stu-id="48188-199">Select **New policy**.</span></span>

4. <span data-ttu-id="48188-200">Onder **toewijzingen**, selecteer **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="48188-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="48188-201">Gebruik de **opnemen** en **uitsluiten** tabbladen om op te geven welke gebruikers en groepen worden beheerd door het beleid.</span><span class="sxs-lookup"><span data-stu-id="48188-201">Use the **Include** and     **Exclude** tabs to specify which users and groups will be managed by the policy.</span></span>

5. <span data-ttu-id="48188-202">Onder **toewijzingen**, selecteer **Cloud-apps.**</span><span class="sxs-lookup"><span data-stu-id="48188-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="48188-203">Kies voor **omvatten alle cloud-apps**.</span><span class="sxs-lookup"><span data-stu-id="48188-203">Choose to **include All cloud apps**.</span></span>
6.  <span data-ttu-id="48188-204">Onder **toegangscontroles**, selecteer **Grant**.</span><span class="sxs-lookup"><span data-stu-id="48188-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="48188-205">Kies **meervoudige authenticatie**.</span><span class="sxs-lookup"><span data-stu-id="48188-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="48188-206">Schakel **beleid inschakelen** naar **op** en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="48188-206">Turn **Enable policy** to **On** and then select **Save**.</span></span>

<span data-ttu-id="48188-207">Voor informatie over het configureren van Azure MFA-instellingen voor Fraudewaarschuwingen instellen, eenmalig overslaan te maken, aangepaste spraakberichten gebruiken, caching configureren, goedgekeurde IP-adressen opgeven, app-wachtwoorden maken, schakelt u MFA onthouden voor apparaten die gebruikers vertrouwt, en selecteer verificatiemethoden, Zie [Azure multi-factor Authentication-instellingen configureren.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="48188-207">For information on how to configure Azure MFA settings to set up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="48188-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48188-208">Next steps</span></span>

- [<span data-ttu-id="48188-209">Bevoegde toegang beveiligen in Azure AD</span><span class="sxs-lookup"><span data-stu-id="48188-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="48188-210">Veelgestelde vragen over Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="48188-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="48188-211">Probleemoplossing voor toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="48188-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="48188-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="48188-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
