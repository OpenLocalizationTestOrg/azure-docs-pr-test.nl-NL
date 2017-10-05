---
title: Technische documentatie van Azure Active Directory voorwaardelijke toegang | Microsoft Docs
description: "Met voorwaardelijk toegangsbeheer controleert de Azure Active Directory de specifieke voorwaarden die u kiest bij het verifiëren van de gebruiker en alvorens deze toegang tot de toepassing. Als deze voorwaarden is voldaan, wordt de gebruiker geverifieerd en toegang te krijgen tot de toepassing."
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="e692a-104">Technische documentatie van Azure Active Directory voorwaardelijke toegang</span><span class="sxs-lookup"><span data-stu-id="e692a-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="e692a-105">Services met voorwaardelijke toegang ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="e692a-105">Services enabled with conditional access</span></span>

<span data-ttu-id="e692a-106">Regels voor voorwaardelijke toegang worden ondersteund tussen de verschillende typen voor Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e692a-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="e692a-107">Deze lijst bevat:</span><span class="sxs-lookup"><span data-stu-id="e692a-107">This list includes:</span></span>


* <span data-ttu-id="e692a-108">Toepassingen die zijn geregistreerd bij de toepassingsproxy van Azure</span><span class="sxs-lookup"><span data-stu-id="e692a-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="e692a-109">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e692a-109">Azure Remote App</span></span>
* <span data-ttu-id="e692a-110">Ontwikkelde line-of-business- en multitenant-toepassingen die zijn geregistreerd bij Azure AD</span><span class="sxs-lookup"><span data-stu-id="e692a-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="e692a-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="e692a-111">Dynamics CRM</span></span>
* <span data-ttu-id="e692a-112">Federatieve toepassingen uit de galerie van Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="e692a-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="e692a-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="e692a-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="e692a-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="e692a-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="e692a-115">Microsoft Office 365 SharePoint Online (inclusief OneDrive voor bedrijven)</span><span class="sxs-lookup"><span data-stu-id="e692a-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="e692a-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="e692a-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="e692a-117">Wachtwoord SSO-toepassingen uit de galerie van Azure AD-toepassing</span><span class="sxs-lookup"><span data-stu-id="e692a-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="e692a-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="e692a-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="e692a-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e692a-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="e692a-120">Toegangsregels inschakelen</span><span class="sxs-lookup"><span data-stu-id="e692a-120">Enable access rules</span></span>
<span data-ttu-id="e692a-121">Elke regel worden ingeschakeld of uitgeschakeld voor een per toepassing basissen.</span><span class="sxs-lookup"><span data-stu-id="e692a-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="e692a-122">Wanneer regels zijn **ON** wordt ingeschakeld en afgedwongen voor gebruikers die toegang tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e692a-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="e692a-123">Wanneer ze zijn **OFF** ze worden niet gebruikt en heeft geen invloed op de aanmeldingsprocedure gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e692a-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="e692a-124">Regels toepassen op specifieke gebruikers</span><span class="sxs-lookup"><span data-stu-id="e692a-124">Applying rules to specific users</span></span>
<span data-ttu-id="e692a-125">Regels kunnen worden toegepast op bepaalde groepen gebruikers op basis van de beveiligingsgroep door in te stellen **toepassen op**.</span><span class="sxs-lookup"><span data-stu-id="e692a-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="e692a-126">**Toepassen op** kan worden ingesteld op **alle gebruikers** of **groepen**.</span><span class="sxs-lookup"><span data-stu-id="e692a-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="e692a-127">Als de waarde **alle gebruikers** regels geldt voor elke gebruiker met toegang tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e692a-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="e692a-128">De **groepen** optie specifieke beveiligings- en distributiegroepen worden geselecteerd, kunnen regels alleen afgedwongen voor deze groepen.</span><span class="sxs-lookup"><span data-stu-id="e692a-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="e692a-129">Bij het implementeren van een regel wordt het meestal eerst deze een beperkte set van gebruikers die lid van een pilot-groepen zijn toe te passen.</span><span class="sxs-lookup"><span data-stu-id="e692a-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="e692a-130">Nadat de regel kan worden toegepast op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e692a-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="e692a-131">Hierdoor wordt de regel moeten worden afgedwongen voor alle gebruikers in de organisatie.</span><span class="sxs-lookup"><span data-stu-id="e692a-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="e692a-132">Selecteer groepen kunnen ook worden vrijgesteld van beleid voor gebruik van de **behalve** optie.</span><span class="sxs-lookup"><span data-stu-id="e692a-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="e692a-133">Leden van deze groepen worden vrijgesteld, zelfs als ze worden weergegeven in een opgenomen groep.</span><span class="sxs-lookup"><span data-stu-id="e692a-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="e692a-134">'Op het werk' netwerken</span><span class="sxs-lookup"><span data-stu-id="e692a-134">“At work” networks</span></span>
<span data-ttu-id="e692a-135">Regels voor voorwaardelijke toegang met een netwerk 'op het werk' afhankelijk zijn van vertrouwde IP-adresbereiken die zijn geconfigureerd in Azure AD, of gebruik van de claim 'binnen corpnet' vanaf AD FS.</span><span class="sxs-lookup"><span data-stu-id="e692a-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="e692a-136">Deze regelgeving omvat:</span><span class="sxs-lookup"><span data-stu-id="e692a-136">These rules include:</span></span>

* <span data-ttu-id="e692a-137">Meervoudige authenticatie niet op het werk</span><span class="sxs-lookup"><span data-stu-id="e692a-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="e692a-138">De toegang niet op het werk blokkeren</span><span class="sxs-lookup"><span data-stu-id="e692a-138">Block access when not at work</span></span>

<span data-ttu-id="e692a-139">Opties voor het opgeven 'op het werk' netwerken</span><span class="sxs-lookup"><span data-stu-id="e692a-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="e692a-140">Configureren van vertrouwde IP-adresbereiken in de [configuratiepagina multi-factorauthenticatie](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="e692a-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="e692a-141">Beleid voor voorwaardelijke toegang gebruiken de geconfigureerde bereiken op elk authenticatie-aanvraag en de uitgifte van tokens voor regels evalueren.</span><span class="sxs-lookup"><span data-stu-id="e692a-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="e692a-142">Gebruik van de binnen configureren corpnet claim deze optie kan worden gebruikt met federatieve-adreslijsten, met AD FS.</span><span class="sxs-lookup"><span data-stu-id="e692a-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="e692a-143">Voor meer informatie over de binnen corpnet claims, Zie [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="e692a-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="e692a-144">Regels op basis van de toepassing gevoeligheid</span><span class="sxs-lookup"><span data-stu-id="e692a-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="e692a-145">Regels worden geconfigureerd per toepassing zodat de hoogwaardige services zonder enige impact op de toegang tot andere services worden beveiligd.</span><span class="sxs-lookup"><span data-stu-id="e692a-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="e692a-146">Regels voor voorwaardelijke toegang kunnen worden geconfigureerd op de **configureren** tabblad van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e692a-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="e692a-147">Regels die momenteel worden aangeboden:</span><span class="sxs-lookup"><span data-stu-id="e692a-147">Rules currently offered:</span></span>

* <span data-ttu-id="e692a-148">**Meervoudige authenticatie**</span><span class="sxs-lookup"><span data-stu-id="e692a-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="e692a-149">Alle gebruikers die dit beleid wordt toegepast op worden te verifiëren via ten minste eenmaal meervoudige verificatie.</span><span class="sxs-lookup"><span data-stu-id="e692a-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="e692a-150">**Meervoudige authenticatie niet op het werk**</span><span class="sxs-lookup"><span data-stu-id="e692a-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="e692a-151">Als dit beleid wordt toegepast, worden alle gebruikers moeten multi-factor authentication-server ten minste eenmaal hebt uitgevoerd als ze vanaf een externe locatie voor niet-werk toegang de service tot.</span><span class="sxs-lookup"><span data-stu-id="e692a-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="e692a-152">Als ze van een werk naar externe locatie, worden ze vereist multifactor-verificatie uitvoeren bij het openen van de service.</span><span class="sxs-lookup"><span data-stu-id="e692a-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="e692a-153">**De toegang niet op het werk blokkeren**</span><span class="sxs-lookup"><span data-stu-id="e692a-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="e692a-154">Wanneer gebruikers naar een externe locatie van het werk verplaatsen, wordt deze geblokkeerd als het beleid 'Toegang niet op het werk blokkeren' op ze is toegepast.</span><span class="sxs-lookup"><span data-stu-id="e692a-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="e692a-155">Ze worden opnieuw kunnen wanneer op een locatie werk toegang.</span><span class="sxs-lookup"><span data-stu-id="e692a-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="e692a-156">Verwante onderwerpen</span><span class="sxs-lookup"><span data-stu-id="e692a-156">Related topics</span></span>
* [<span data-ttu-id="e692a-157">Beveiligen van toegang tot Office 365 en andere apps die zijn verbonden met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e692a-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* <span data-ttu-id="e692a-158">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="e692a-158">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>

