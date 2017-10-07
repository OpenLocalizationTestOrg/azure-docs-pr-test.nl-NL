---
title: technische documentatie voor voorwaardelijke toegang van Active Directory aaaAzure | Microsoft Docs
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory Hallo bepaalde voorwaarden die u bij het verifiëren van de gebruiker Hallo en alvorens deze toegang toohello toepassing kiezen. Als deze voorwaarden is voldaan, wordt Hallo gebruiker geverifieerd en toegang toohello toepassing toegestaan."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="17000-104">Technische documentatie van Azure Active Directory voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="17000-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="17000-105">Services met voorwaardelijke toegang ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="17000-105">Services enabled with conditional access</span></span>

<span data-ttu-id="17000-106">Regels voor voorwaardelijke toegang worden ondersteund tussen de verschillende typen voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="17000-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="17000-107">Deze lijst bevat:</span><span class="sxs-lookup"><span data-stu-id="17000-107">This list includes:</span></span>


* <span data-ttu-id="17000-108">Toepassingen die zijn geregistreerd bij hello Azure-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="17000-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="17000-109">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="17000-109">Azure Remote App</span></span>
* <span data-ttu-id="17000-110">Ontwikkelde line-of-business- en multitenant-toepassingen die zijn geregistreerd bij Azure AD</span><span class="sxs-lookup"><span data-stu-id="17000-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="17000-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="17000-111">Dynamics CRM</span></span>
* <span data-ttu-id="17000-112">Federatieve toepassingen van hello Azure AD-toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="17000-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="17000-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="17000-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="17000-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="17000-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="17000-115">Microsoft Office 365 SharePoint Online (inclusief OneDrive voor bedrijven)</span><span class="sxs-lookup"><span data-stu-id="17000-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="17000-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="17000-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="17000-117">Wachtwoord SSO-toepassingen van hello Azure AD-toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="17000-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="17000-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="17000-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="17000-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="17000-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="17000-120">Toegangsregels inschakelen</span><span class="sxs-lookup"><span data-stu-id="17000-120">Enable access rules</span></span>
<span data-ttu-id="17000-121">Elke regel worden ingeschakeld of uitgeschakeld voor een per toepassing basissen.</span><span class="sxs-lookup"><span data-stu-id="17000-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="17000-122">Wanneer regels zijn **ON** wordt ingeschakeld en voor gebruikers die toegang tot de toepassing hello afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="17000-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="17000-123">Wanneer ze zijn **OFF** wordt niet gebruikt en wordt niet impact Hallo gebruikers zich aanmelden ervaring.</span><span class="sxs-lookup"><span data-stu-id="17000-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="17000-124">Toepassen van regels toospecific gebruikers</span><span class="sxs-lookup"><span data-stu-id="17000-124">Applying rules toospecific users</span></span>
<span data-ttu-id="17000-125">Regels kunnen worden toegepast toospecific sets van gebruikers op basis van de beveiligingsgroep door in te stellen **toepassen op**.</span><span class="sxs-lookup"><span data-stu-id="17000-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="17000-126">**Toepassen op** te kunnen worden ingesteld**alle gebruikers** of **groepen**.</span><span class="sxs-lookup"><span data-stu-id="17000-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="17000-127">Als de waarde te**alle gebruikers** Hallo regels gelden tooany gebruiker met toegang toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="17000-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="17000-128">Hallo **groepen** optie specifieke beveiligings- en distributiepunten groepen toobe is geselecteerd, kunnen regels alleen afgedwongen voor deze groepen.</span><span class="sxs-lookup"><span data-stu-id="17000-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="17000-129">Bij het implementeren van een regel, is het gebruikelijk dat toofirst toepassen een beperkt aantal gebruikers die lid van een pilot-groepen zijn.</span><span class="sxs-lookup"><span data-stu-id="17000-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="17000-130">Zodra de volledige Hallo regel te kan worden toegepast**alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="17000-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="17000-131">Hierdoor wordt toobe afgedwongen voor alle gebruikers in de organisatie Hallo Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="17000-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="17000-132">Selecteer groepen kunnen ook worden vrijgesteld van met behulp van Hallo **behalve** optie.</span><span class="sxs-lookup"><span data-stu-id="17000-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="17000-133">Leden van deze groepen worden vrijgesteld, zelfs als ze worden weergegeven in een opgenomen groep.</span><span class="sxs-lookup"><span data-stu-id="17000-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="17000-134">'Op het werk' netwerken</span><span class="sxs-lookup"><span data-stu-id="17000-134">“At work” networks</span></span>
<span data-ttu-id="17000-135">Regels voor voorwaardelijke toegang met een netwerk 'op het werk' afhankelijk zijn van vertrouwde IP-adresbereiken die zijn geconfigureerd in Azure AD of het gebruik van Hallo 'binnen corpnet' claim vanaf AD FS.</span><span class="sxs-lookup"><span data-stu-id="17000-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="17000-136">Deze regelgeving omvat:</span><span class="sxs-lookup"><span data-stu-id="17000-136">These rules include:</span></span>

* <span data-ttu-id="17000-137">Meervoudige authenticatie niet op het werk</span><span class="sxs-lookup"><span data-stu-id="17000-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="17000-138">De toegang niet op het werk blokkeren</span><span class="sxs-lookup"><span data-stu-id="17000-138">Block access when not at work</span></span>

<span data-ttu-id="17000-139">Opties voor het opgeven 'op het werk' netwerken</span><span class="sxs-lookup"><span data-stu-id="17000-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="17000-140">Configureren van vertrouwde IP-adresbereiken in Hallo [configuratiepagina multi-factorauthenticatie](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="17000-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="17000-141">Beleid voor voorwaardelijke toegang gebruikt op elke aanvraag en -token uitgifte tooevaluate verificatieregels Hallo geconfigureerd bereiken.</span><span class="sxs-lookup"><span data-stu-id="17000-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="17000-142">Gebruik van Hallo binnen corpnet claim configureren, deze optie kan worden gebruikt met federatieve-adreslijsten, met AD FS.</span><span class="sxs-lookup"><span data-stu-id="17000-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="17000-143">toolearn meer informatie over Hallo binnen corpnet claims, Zie [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="17000-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="17000-144">Regels op basis van de toepassing gevoeligheid</span><span class="sxs-lookup"><span data-stu-id="17000-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="17000-145">Regels worden geconfigureerd per toepassing hello hoogwaardige services toobe beveiligd zonder enige impact op tooother toegangsservices toe.</span><span class="sxs-lookup"><span data-stu-id="17000-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="17000-146">Regels voor voorwaardelijke toegang kunnen worden geconfigureerd op Hallo **configureren** tabblad van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="17000-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="17000-147">Regels die momenteel worden aangeboden:</span><span class="sxs-lookup"><span data-stu-id="17000-147">Rules currently offered:</span></span>

* <span data-ttu-id="17000-148">**Meervoudige authenticatie**</span><span class="sxs-lookup"><span data-stu-id="17000-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="17000-149">Alle gebruikers die dit beleid toegepast toowill is vereist tooauthenticate via multi-factor authentication-server ten minste één keer worden.</span><span class="sxs-lookup"><span data-stu-id="17000-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="17000-150">**Meervoudige authenticatie niet op het werk**</span><span class="sxs-lookup"><span data-stu-id="17000-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="17000-151">Als dit beleid wordt toegepast, worden alle gebruikers vereiste toohave uitgevoerd multi-factor authentication-server ten minste eenmaal als ze toegang krijgen Hallo service vanaf een externe locatie niet werken tot.</span><span class="sxs-lookup"><span data-stu-id="17000-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="17000-152">Als ze vanaf een locatie van de tooremote werk verplaatst, worden deze vereiste tooperform multifactor-verificatie bij het openen van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="17000-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="17000-153">**De toegang niet op het werk blokkeren**</span><span class="sxs-lookup"><span data-stu-id="17000-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="17000-154">Wanneer gebruikers van werk tooa externe locatie worden verplaatst, wordt deze geblokkeerd als Hallo 'Toegang niet op het werk blokkeren' beleid is toegepast toothem.</span><span class="sxs-lookup"><span data-stu-id="17000-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="17000-155">Ze worden opnieuw kunnen wanneer op een locatie werk toegang.</span><span class="sxs-lookup"><span data-stu-id="17000-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="17000-156">Verwante onderwerpen</span><span class="sxs-lookup"><span data-stu-id="17000-156">Related topics</span></span>
* [<span data-ttu-id="17000-157">Toegang beveiligen tooOffice 365 en andere apps verbonden tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17000-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* <span data-ttu-id="17000-158">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="17000-158">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>

