---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: Meer informatie over hoe Azure AD Identity Protection kunt u de mogelijkheid van een aanvaller misbruik maakt van een verdachte identiteit of het apparaat en voor het beveiligen van een identiteit of een apparaat dat eerder is verdacht of bekend is dat inbreuk wordt gepleegd beperken.
services: active-directory
keywords: beveiliging in Azure active directory-identiteit, cloud app discovery, het beheren van toepassingen, beveiliging, risico, risiconiveau, beveiligingsprobleem, beveiligingsbeleid
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="02319-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="02319-105">Azure Active Directory: Identity Protection is een functie van de Azure AD Premium P2-versie waarmee u kunt:</span><span class="sxs-lookup"><span data-stu-id="02319-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="02319-106">Detecteren van mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie</span><span class="sxs-lookup"><span data-stu-id="02319-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="02319-107">Automatische antwoorden op gedetecteerde verdachte acties die zijn gekoppeld aan de identiteiten van uw organisatie configureren</span><span class="sxs-lookup"><span data-stu-id="02319-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="02319-108">Verdachte incidenten onderzoeken en onderneem gepaste actie deze op te lossen</span><span class="sxs-lookup"><span data-stu-id="02319-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="02319-109">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="02319-109">Getting started</span></span>

<span data-ttu-id="02319-110">Microsoft beveiligt cloud-gebaseerde identiteiten voor meer dan een tien jaar.</span><span class="sxs-lookup"><span data-stu-id="02319-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="02319-111">Met Azure Active Directory: Identity Protection kunt in uw omgeving, u de dezelfde systemen ter bescherming van die Microsoft gebruikt voor het beveiligen van identiteiten.</span><span class="sxs-lookup"><span data-stu-id="02319-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="02319-112">De meeste beveiligingslekken plaatsvinden als aanvallers toegang krijgen tot een omgeving met de identiteit van een gebruiker te stelen.</span><span class="sxs-lookup"><span data-stu-id="02319-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="02319-113">In de afgelopen jaren, zijn aanvallers steeds effectief gebruik van schendingen van derden en het gebruik van geavanceerde phishingaanvallen geworden.</span><span class="sxs-lookup"><span data-stu-id="02319-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="02319-114">Als een aanvaller toegang tot het zelfs als deze gebruiker met laag bevoegde accounts krijgt, is het relatief gemakkelijk voor hen toegang te krijgen tot bronnen van belangrijke bedrijfsgegevens via laterale verplaatsing.</span><span class="sxs-lookup"><span data-stu-id="02319-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="02319-115">Als gevolg hiervan moet u:</span><span class="sxs-lookup"><span data-stu-id="02319-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="02319-116">Beveiligen van alle identiteiten ongeacht hun machtigingsniveau</span><span class="sxs-lookup"><span data-stu-id="02319-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="02319-117">Proactief te voorkomen dat waarmee is geknoeid identiteiten geschonden</span><span class="sxs-lookup"><span data-stu-id="02319-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="02319-118">Detectie van verdachte identiteiten is geen eenvoudige taak.</span><span class="sxs-lookup"><span data-stu-id="02319-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="02319-119">Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en identiteiten waarmee is geknoeid methodiek voor het detecteren van afwijkingen en verdachte incidenten die mogelijk aangeven.</span><span class="sxs-lookup"><span data-stu-id="02319-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="02319-120">Met deze gegevens Identity Protection genereert rapporten en waarschuwingen waarmee u kunt de gedetecteerde problemen evalueren en juiste risicobeperking of herstelacties duren.</span><span class="sxs-lookup"><span data-stu-id="02319-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="02319-121">Azure Active Directory: Identity Protection is meer dan een controle en rapportage.</span><span class="sxs-lookup"><span data-stu-id="02319-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="02319-122">Ter bescherming van uw organisatie identiteiten, kunt u risico-beleidsregels die automatisch op gedetecteerde problemen reageren als een opgegeven risiconiveau is bereikt.</span><span class="sxs-lookup"><span data-stu-id="02319-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="02319-123">Deze beleidsregels, naast de andere besturingselementen voorwaardelijke toegang is verstrekt door Azure Active Directory en EMS, kunnen automatisch blokkeren of initiëren adaptieve herstelacties met inbegrip van wachtwoorden opnieuw instellen en afdwingen van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="02319-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="02319-124">Mogelijkheden voor preventie van identiteit</span><span class="sxs-lookup"><span data-stu-id="02319-124">Identity Protection capabilities</span></span>

<span data-ttu-id="02319-125">**Detecteren van zwakke plekken en riskant accounts:**</span><span class="sxs-lookup"><span data-stu-id="02319-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="02319-126">Aangepaste aanbevelingen voor de algehele beveiligingsstatus markeert beveiligingslekken bieden</span><span class="sxs-lookup"><span data-stu-id="02319-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="02319-127">Aanmelden risiconiveaus berekenen</span><span class="sxs-lookup"><span data-stu-id="02319-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="02319-128">Gebruiker risiconiveaus berekenen</span><span class="sxs-lookup"><span data-stu-id="02319-128">Calculating user risk levels</span></span>


<span data-ttu-id="02319-129">**Bezig met het onderzoeken van risico's:**</span><span class="sxs-lookup"><span data-stu-id="02319-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="02319-130">Verzenden van meldingen voor risico 's</span><span class="sxs-lookup"><span data-stu-id="02319-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="02319-131">Het onderzoeken van risico's met behulp van de relevante en contextuele informatie</span><span class="sxs-lookup"><span data-stu-id="02319-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="02319-132">Biedt eenvoudige werkstromen voor het bijhouden van onderzoeken</span><span class="sxs-lookup"><span data-stu-id="02319-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="02319-133">Eenvoudige toegang tot herstelacties zoals het wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="02319-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="02319-134">**Beleid voor voorwaardelijke toegang op basis van risico's:**</span><span class="sxs-lookup"><span data-stu-id="02319-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="02319-135">Beleid voor riskante aanmeldingen beperken door aanmeldingen blokkeren of uitdagingen voor meervoudige verificatie vereisen.</span><span class="sxs-lookup"><span data-stu-id="02319-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="02319-136">Beleid voor het blokkeren of beveiligde riskant gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="02319-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="02319-137">Beleid voor gebruikers moeten zich registreren voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="02319-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="02319-138">Identity Protection-functies</span><span class="sxs-lookup"><span data-stu-id="02319-138">Identity Protection roles</span></span>

<span data-ttu-id="02319-139">Taakverdeling van de beheertaken voor uw implementatie Identity Protection kunt u verschillende rollen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="02319-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="02319-140">Azure AD Identity Protection ondersteunt 3 directory-functies:</span><span class="sxs-lookup"><span data-stu-id="02319-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="02319-141">Rol</span><span class="sxs-lookup"><span data-stu-id="02319-141">Role</span></span>                         | <span data-ttu-id="02319-142">Kan doen</span><span class="sxs-lookup"><span data-stu-id="02319-142">Can do</span></span>                          | <span data-ttu-id="02319-143">Is niet mogelijk</span><span class="sxs-lookup"><span data-stu-id="02319-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="02319-144">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="02319-144">Global administrator</span></span>         | <span data-ttu-id="02319-145">Volledige toegang tot Identity Protection, vrijgeven Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="02319-146">Beveiligingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="02319-146">Security administrator</span></span>       | <span data-ttu-id="02319-147">Volledige toegang tot Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-147">Full access to Identity Protection</span></span> | <span data-ttu-id="02319-148">Ingebouwde Identity Protection, wachtwoorden opnieuw instellen voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="02319-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="02319-149">Beveiligingslezer</span><span class="sxs-lookup"><span data-stu-id="02319-149">Security reader</span></span>              | <span data-ttu-id="02319-150">Gereed alleen toegang tot Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="02319-151">Ingebouwde Identity Protection, remidiate gebruikers,-beleid configureren, wachtwoorden opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="02319-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="02319-152">Zie voor meer informatie [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="02319-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="02319-153">Detectie</span><span class="sxs-lookup"><span data-stu-id="02319-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="02319-154">Beveiligingsproblemen</span><span class="sxs-lookup"><span data-stu-id="02319-154">Vulnerabilities</span></span>

<span data-ttu-id="02319-155">Azure Active Directory: Identity Protection analyses van uw configuratie en beveiligingsproblemen die invloed op uw gebruikers-id's hebben kunnen detecteert.</span><span class="sxs-lookup"><span data-stu-id="02319-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="02319-156">Zie voor meer informatie [beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="02319-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="02319-157">Risico 's</span><span class="sxs-lookup"><span data-stu-id="02319-157">Risk events</span></span>

<span data-ttu-id="02319-158">Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek voor het detecteren van verdachte acties die zijn gerelateerd aan uw gebruikers-id's.</span><span class="sxs-lookup"><span data-stu-id="02319-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="02319-159">Maakt een record voor elke gedetecteerde verdachte actie van het systeem.</span><span class="sxs-lookup"><span data-stu-id="02319-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="02319-160">Deze records worden ook wel bekend als risico's.</span><span class="sxs-lookup"><span data-stu-id="02319-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="02319-161">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02319-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="02319-162">Onderzoek</span><span class="sxs-lookup"><span data-stu-id="02319-162">Investigation</span></span>
<span data-ttu-id="02319-163">Uw reis door Identity Protection wordt doorgaans begint met het Identity Protection-dashboard.</span><span class="sxs-lookup"><span data-stu-id="02319-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="02319-164">![Herstel](./media/active-directory-identityprotection/1000.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="02319-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="02319-165">Het dashboard biedt die u toegang tot:</span><span class="sxs-lookup"><span data-stu-id="02319-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="02319-166">Rapporten, zoals **gebruikers die zijn gemarkeerd voor risico**, **bestaat de kans dat gebeurtenissen** en **beveiligingsproblemen**</span><span class="sxs-lookup"><span data-stu-id="02319-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="02319-167">Instellingen zoals de configuratie van uw **beveiligingsbeleid**, **meldingen** en **multi-factor authentication-registratie**</span><span class="sxs-lookup"><span data-stu-id="02319-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="02319-168">Is doorgaans het beginpunt voor onderzoek, het proces is van het controleren van de activiteiten, logboeken en andere relevante informatie die betrekking hebben op een risicogebeurtenis om te bepalen of de updateherstel- of risicobeperking stappen nodig zijn, en hoe de identiteit is geknoeid en begrijpen hoe de identiteit van de verdachte is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="02319-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="02319-169">U kunt verbinden, de onderzoeksactiviteiten van uw naar het [meldingen](active-directory-identityprotection-notifications.md) Azure Active Directory Protection per e-mail verzendt.</span><span class="sxs-lookup"><span data-stu-id="02319-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="02319-170">De volgende secties bieden u meer informatie en de stappen die zijn gerelateerd aan een onderzoek.</span><span class="sxs-lookup"><span data-stu-id="02319-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="02319-171">Riskant aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="02319-171">Risky sign-ins</span></span>

<span data-ttu-id="02319-172">Azure Active Directory detecteert [risico gebeurtenistypen](active-directory-reporting-risk-events.md#risk-event-types) in realtime en offline.</span><span class="sxs-lookup"><span data-stu-id="02319-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="02319-173">Elke risicogebeurtenis dat is aangetroffen voor een aanmelding van een gebruiker bijdraagt aan een logisch concept is aangeroepen riskant aanmelden.</span><span class="sxs-lookup"><span data-stu-id="02319-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="02319-174">Een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk niet uitgevoerd door de legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="02319-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="02319-175">Aanmelden risiconiveau</span><span class="sxs-lookup"><span data-stu-id="02319-175">Sign-in risk level</span></span>

<span data-ttu-id="02319-176">Een risiconiveau aanmelden is een indicatie (hoog, Gemiddeld of laag) van de kans op een aanmeldingspoging is niet uitgevoerd door de legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="02319-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="02319-177">Beperkende aanmelden risico 's</span><span class="sxs-lookup"><span data-stu-id="02319-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="02319-178">Een beperking is een actie die de mogelijkheid van een aanvaller misbruik maakt van een verdachte identiteit of het apparaat zonder dat de identiteit of het apparaat hersteld naar een veilige status beperken.</span><span class="sxs-lookup"><span data-stu-id="02319-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="02319-179">Een risicobeperking vorige aanmelden risicogebeurtenissen die zijn gekoppeld aan de identiteit of het apparaat niet is opgelost.</span><span class="sxs-lookup"><span data-stu-id="02319-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="02319-180">U kunt aanmelden risico beveiliging policicies configureren riskant aanmeldingen automatisch om's te beperken.</span><span class="sxs-lookup"><span data-stu-id="02319-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="02319-181">Met deze beleidsregels, u rekening houden met het risiconiveau van de gebruiker of de aanmeldingspagina riskant aanmeldingen wordt geblokkeerd of dat de gebruiker naar de multi-factor authentication uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="02319-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="02319-182">Deze acties kunnen voorkomen dat een aanvaller gebruikmaakt van de identiteit van een gestolen om te leiden tot beschadiging en mogelijk hebt u enige tijd voor het beveiligen van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="02319-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="02319-183">Beveiligingsbeleid Aanmelden risico</span><span class="sxs-lookup"><span data-stu-id="02319-183">Sign-in risk security policy</span></span>
<span data-ttu-id="02319-184">Een beleid voor aanmelden risico is een beleid voor voorwaardelijke toegang dat het risico op een specifieke aanmelden wordt geëvalueerd en oplossingen op basis van vooraf gedefinieerde voorwaarden en regels van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="02319-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="02319-185">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1014.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="02319-186">Azure AD Identity Protection helpt die u bij het beheren van het beperken van riskante aanmeldingen doordat u:</span><span class="sxs-lookup"><span data-stu-id="02319-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="02319-187">Stel de gebruikers en groepen die het beleid van toepassing:</span><span class="sxs-lookup"><span data-stu-id="02319-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="02319-188">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1015.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="02319-189">Stel de aanmeldingspagina risico niveau drempelwaarde (laag, Gemiddeld of hoog) waarmee het beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="02319-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="02319-190">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1016.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="02319-191">Stel de besturingselementen om te worden afgedwongen wanneer het beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="02319-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="02319-192">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1017.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="02319-193">De status van uw beleid switch:</span><span class="sxs-lookup"><span data-stu-id="02319-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="02319-194">![Registratieprocedure voor MFA](./media/active-directory-identityprotection/403.png "registratieprocedure voor MFA")</span><span class="sxs-lookup"><span data-stu-id="02319-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="02319-195">Bekijken en evalueren van de gevolgen van een wijziging voordat u deze activeert:</span><span class="sxs-lookup"><span data-stu-id="02319-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="02319-196">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1018.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="02319-197">Wat u moet weten</span><span class="sxs-lookup"><span data-stu-id="02319-197">What you need to know</span></span>
<span data-ttu-id="02319-198">U kunt een beveiligingsbeleid Aanmelden risico meervoudige authenticatie configureren:</span><span class="sxs-lookup"><span data-stu-id="02319-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="02319-199">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1017.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="02319-200">Echter, uit veiligheidsoverwegingen deze instelling werkt alleen voor gebruikers die al zijn geregistreerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="02319-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="02319-201">Als de voorwaarde voor meervoudige authenticatie voor een gebruiker die nog niet is geregistreerd voor multi-factor authentication is voldaan, wordt de gebruiker is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="02319-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="02319-202">Als het wordt aanbevolen als u wilt meervoudige verificatie vereisen voor riskante aanmeldingen, moet u:</span><span class="sxs-lookup"><span data-stu-id="02319-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="02319-203">Schakel de [registratiebeleid voor meervoudige verificatie](#multi-factor-authentication-registration-policy) voor de betrokken gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02319-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="02319-204">Vereisen dat de betrokken gebruikers aanmelding in een niet-riskant sessie een MFA-registratie uitvoeren</span><span class="sxs-lookup"><span data-stu-id="02319-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="02319-205">U deze stappen uitvoert, zorgt u ervoor dat meervoudige verificatie is vereist voor een riskante aanmelden.</span><span class="sxs-lookup"><span data-stu-id="02319-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="02319-206">Aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="02319-206">Best practices</span></span>
<span data-ttu-id="02319-207">U kiest een **hoge** drempelwaarde vermindert het aantal keer dat een beleid wordt geactiveerd en minimaliseert de overlast voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02319-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="02319-208">Echter, worden uitgesloten **laag** en **gemiddeld** aanmeldingen gemarkeerd voor risico's van het beleid, dat een aanvaller gebruikmaakt van de identiteit van een verdachte kan niet worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="02319-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="02319-209">Bij het instellen van het beleid</span><span class="sxs-lookup"><span data-stu-id="02319-209">When setting the policy,</span></span>

* <span data-ttu-id="02319-210">Gebruikers die geen / multi-factor authentication-server kunnen geen uitsluiten</span><span class="sxs-lookup"><span data-stu-id="02319-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="02319-211">Gebruikers in landen waar het inschakelen van het beleid is het niet praktisch uitsluiten (bijvoorbeeld geen toegang tot de helpdesk)</span><span class="sxs-lookup"><span data-stu-id="02319-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="02319-212">Voorkomen dat gebruikers die waarschijnlijk voor het genereren van een groot aantal ONWAAR-positieven (ontwikkelaars, beveiligingsanalisten)</span><span class="sxs-lookup"><span data-stu-id="02319-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="02319-213">Gebruik een **hoge** drempelwaarde tijdens de eerste beleid implementeert, of als u uitdagingen die zichtbaar zijn voor eindgebruikers minimaliseert.</span><span class="sxs-lookup"><span data-stu-id="02319-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="02319-214">Gebruik een **laag** drempelwaarde als uw organisatie betere beveiliging vereist.</span><span class="sxs-lookup"><span data-stu-id="02319-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="02319-215">Als u een **laag** drempelwaarde introduceert extra gebruiker aanmelden uitdagingen, maar een hogere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="02319-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="02319-216">De aanbevolen standaardwaarde voor de meeste organisaties is het configureren van een regel voor een **gemiddeld** drempelwaarde een evenwicht tot stand tussen bruikbaarheid en veiligheid.</span><span class="sxs-lookup"><span data-stu-id="02319-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="02319-217">Het beleid voor aanmelden risico is:</span><span class="sxs-lookup"><span data-stu-id="02319-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="02319-218">Toegepast op alle browserverkeer en aanmeldingen die moderne authenticatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02319-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="02319-219">Niet toegepast op toepassingen met behulp van beveiligingsprotocollen voor oudere door het WS-Trust-eindpunt op de federatieve IDP, zoals ADFS uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="02319-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="02319-220">De **Risicogebeurtenissen** pagina in de console Identity Protection worden alle gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="02319-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="02319-221">Dit beleid is toegepast</span><span class="sxs-lookup"><span data-stu-id="02319-221">This policy was applied to</span></span>
* <span data-ttu-id="02319-222">U kunt bekijken van de activiteit en bepalen of de actie die geschikt of niet is</span><span class="sxs-lookup"><span data-stu-id="02319-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="02319-223">Zie voor een overzicht van de gerelateerde gebruikerservaring:</span><span class="sxs-lookup"><span data-stu-id="02319-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="02319-224">Herstel voor riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="02319-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="02319-225">Riskant aanmelden geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="02319-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="02319-226">Aanmelden-ervaring met Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="02319-227">**Opent het dialoogvenster gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="02319-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="02319-228">Op de **Azure AD Identity Protection** blade in de **configureren** sectie, klikt u op **aanmelden risico beleid**.</span><span class="sxs-lookup"><span data-stu-id="02319-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="02319-229">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1014.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="02319-230">Gebruikers voor wie wordt aangegeven dat ze risico lopen</span><span class="sxs-lookup"><span data-stu-id="02319-230">Users flagged for risk</span></span>

<span data-ttu-id="02319-231">Alle actieve [bestaat de kans dat gebeurtenissen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd door Azure Active Directory voor een gebruiker bijdragen aan een logisch concept is aangeroepen gebruiker risico.</span><span class="sxs-lookup"><span data-stu-id="02319-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="02319-232">Een gebruiker die is gemarkeerd voor risico is een indicator voor een gebruikersaccount die mogelijk zijn aangetast.</span><span class="sxs-lookup"><span data-stu-id="02319-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Gebruikers voor wie wordt aangegeven dat ze risico lopen](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="02319-234">Risiconiveau van gebruiker</span><span class="sxs-lookup"><span data-stu-id="02319-234">User risk level</span></span>

<span data-ttu-id="02319-235">Het risiconiveau van een gebruiker is een indicatie van de kans dat de identiteit van de gebruiker is ingebroken (hoog, Gemiddeld of laag).</span><span class="sxs-lookup"><span data-stu-id="02319-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="02319-236">Deze wordt berekend op basis van de gebruiker risicogebeurtenissen die gekoppeld aan de identiteit van een gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="02319-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="02319-237">De status van een risicogebeurtenis is **Active** of **gesloten**.</span><span class="sxs-lookup"><span data-stu-id="02319-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="02319-238">Alleen het risico van gebeurtenissen die zijn **Active** bijdragen aan de gebruiker risico niveau berekening.</span><span class="sxs-lookup"><span data-stu-id="02319-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="02319-239">Het risiconiveau van de gebruiker wordt berekend met behulp van de volgende invoer:</span><span class="sxs-lookup"><span data-stu-id="02319-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="02319-240">Actieve risicogebeurtenissen die invloed hebben op de gebruiker</span><span class="sxs-lookup"><span data-stu-id="02319-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="02319-241">Risiconiveau van deze gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="02319-241">Risk level of these events</span></span>
* <span data-ttu-id="02319-242">Hiermee wordt aangegeven of welke herstelacties zijn gemaakt</span><span class="sxs-lookup"><span data-stu-id="02319-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="02319-243">![Gebruiker risico's](./media/active-directory-identityprotection/1031.png "gebruiker risico's")</span><span class="sxs-lookup"><span data-stu-id="02319-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="02319-244">U kunt de risiconiveaus gebruiker gebruiken voor het maken van beleid voor voorwaardelijke toegang die riskant gebruikers aanmelden blokkeren of zorgen dat ze veilig hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="02319-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="02319-245">Risico's handmatig sluiten</span><span class="sxs-lookup"><span data-stu-id="02319-245">Closing risk events manually</span></span>

<span data-ttu-id="02319-246">In de meeste gevallen duurt herstelacties zoals een beveiligd wachtwoord opnieuw instellen op automatisch risico's te sluiten.</span><span class="sxs-lookup"><span data-stu-id="02319-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="02319-247">Echter, dit mogelijk niet altijd mogelijk.</span><span class="sxs-lookup"><span data-stu-id="02319-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="02319-248">Dit is, bijvoorbeeld het geval wanneer:</span><span class="sxs-lookup"><span data-stu-id="02319-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="02319-249">Een gebruiker met actieve risicogebeurtenissen is verwijderd</span><span class="sxs-lookup"><span data-stu-id="02319-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="02319-250">Een onderzoek blijkt dat een risicogebeurtenis gemelde heeft zijn uitvoeren door de gebruiker legitieme</span><span class="sxs-lookup"><span data-stu-id="02319-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="02319-251">Omdat de risico's die zijn **Active** bijdragen aan de gebruiker risico berekening, moet u mogelijk handmatig een risiconiveau verlagen door risicogebeurtenissen handmatig sluiten.</span><span class="sxs-lookup"><span data-stu-id="02319-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="02319-252">U kunt kiezen tijdens het onderzoek moet worden uitgevoerd op een van deze acties om de status van een gebeurtenis risico's te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="02319-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="02319-253">![Acties](./media/active-directory-identityprotection/34.png "acties")</span><span class="sxs-lookup"><span data-stu-id="02319-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="02319-254">**Los** - als na een risicogebeurtenis onderzoeken, u een juiste herstelactie buiten Identity Protection heeft ondernomen, en u van mening bent dat de gebeurtenis risico's nodig hebt gesloten, markeert u de gebeurtenis als opgelost.</span><span class="sxs-lookup"><span data-stu-id="02319-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="02319-255">Gebeurtenissen stelt de status van de risicogebeurtenis op gesloten en de risicogebeurtenis wordt niet langer bijdragen aan de gebruiker risico's opgelost.</span><span class="sxs-lookup"><span data-stu-id="02319-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="02319-256">**Markeren als fout-positieve** -In sommige gevallen kan u een risicogebeurtenis onderzoeken en onjuist is gemarkeerd als een riskante te detecteren.</span><span class="sxs-lookup"><span data-stu-id="02319-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="02319-257">Verkleint u het aantal dergelijke instanties door de risicogebeurtenis als fout-positieve markeren.</span><span class="sxs-lookup"><span data-stu-id="02319-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="02319-258">Dit helpt de machine learning-algoritmen ter verbetering van de classificatie van soortgelijke gebeurtenissen in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="02319-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="02319-259">De status van de fout-positieve gebeurtenissen wordt **gesloten** en ze niet langer draagt bij tot het risico van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="02319-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="02319-260">**Negeren** : als u een herstelactie niet genomen, maar u wilt dat de risicogebeurtenis worden verwijderd uit de actieve lijst kunt u een risicogebeurtenis negeren markeren en de gebeurtenisstatus van de wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="02319-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="02319-261">Genegeerd gebeurtenissen bijdragen niet tot het risico van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="02319-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="02319-262">Deze optie dient alleen ongebruikelijke omstandigheden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="02319-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="02319-263">**Opnieuw activeren** -gebeurtenissen die handmatig zijn gesloten risico (door te kiezen **los**, **fout-positief**, of **negeren**) kan opnieuw worden geactiveerd, instellen van de gebeurtenisstatus terug naar **Active**.</span><span class="sxs-lookup"><span data-stu-id="02319-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="02319-264">Opnieuw geactiveerde risicogebeurtenissen bijdragen aan de gebruiker risico niveau berekening.</span><span class="sxs-lookup"><span data-stu-id="02319-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="02319-265">Risico's gesloten via herstel (zoals een beveiligd wachtwoord opnieuw instellen) kunnen niet opnieuw worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="02319-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="02319-266">**Opent het dialoogvenster gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="02319-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="02319-267">Op de **Azure AD Identity Protection** blade onder **onderzoeken**, klikt u op **bestaat de kans dat gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="02319-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="02319-268">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1002.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="02319-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="02319-269">In de **bestaat de kans dat gebeurtenissen** lijst, klikt u op een risico.</span><span class="sxs-lookup"><span data-stu-id="02319-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="02319-270">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1003.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="02319-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="02319-271">Met de rechtermuisknop op een gebruiker op de blade risico.</span><span class="sxs-lookup"><span data-stu-id="02319-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="02319-272">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1004.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="02319-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="02319-273">Alle gebeurtenissen van de risico's voor een gebruiker sluiten handmatig</span><span class="sxs-lookup"><span data-stu-id="02319-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="02319-274">In plaats van handmatig sluiten afzonderlijk risico's voor een gebruiker, biedt Azure Active Directory: Identity Protection u ook een methode voor het sluiten van alle gebeurtenissen voor een gebruiker met één klik.</span><span class="sxs-lookup"><span data-stu-id="02319-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="02319-275">![Acties](./media/active-directory-identityprotection/2222.png "acties")</span><span class="sxs-lookup"><span data-stu-id="02319-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="02319-276">Wanneer u klikt op **sluiten alle gebeurtenissen**, alle gebeurtenissen zijn gesloten en de betrokken gebruiker is niet meer risico.</span><span class="sxs-lookup"><span data-stu-id="02319-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="02319-277">Beveiligingsstatus gebruiker risico 's</span><span class="sxs-lookup"><span data-stu-id="02319-277">Remediating user risk events</span></span>

<span data-ttu-id="02319-278">Een herstel is een actie voor het beveiligen van een identiteit of een apparaat dat eerder verdachte of bekend is mogelijk onveilig.</span><span class="sxs-lookup"><span data-stu-id="02319-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="02319-279">Een herstelactie herstelt u de identiteit of het apparaat naar een veilige status en wordt omgezet vorige risico's die zijn gekoppeld aan de identiteit of het apparaat.</span><span class="sxs-lookup"><span data-stu-id="02319-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="02319-280">Als u wilt herstellen, gebruiker risicogebeurtenissen, kunt u:</span><span class="sxs-lookup"><span data-stu-id="02319-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="02319-281">Uitvoeren van een beveiligd wachtwoord opnieuw instellen op gebruiker risicogebeurtenissen handmatig herstellen</span><span class="sxs-lookup"><span data-stu-id="02319-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="02319-282">Een gebruiker risico security-beleid te beperken of gebruiker risicogebeurtenissen automatisch herstellen configureren</span><span class="sxs-lookup"><span data-stu-id="02319-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="02319-283">Het geïnfecteerde apparaat herstellen met installatiekopie</span><span class="sxs-lookup"><span data-stu-id="02319-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="02319-284">Handmatige beveiligd wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="02319-284">Manual secure password reset</span></span>
<span data-ttu-id="02319-285">Een beveiligd wachtwoord opnieuw instellen is een effectieve herstel voor veel risicogebeurtenissen en wanneer uitgevoerd, sluit u deze risicogebeurtenissen automatisch en het risiconiveau van de gebruiker opnieuw worden berekend.</span><span class="sxs-lookup"><span data-stu-id="02319-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="02319-286">Het Identity Protection-dashboard kunt u een wachtwoord opnieuw instellen voor een riskante gebruiker te initiëren.</span><span class="sxs-lookup"><span data-stu-id="02319-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="02319-287">Het gerelateerde dialoogvenster biedt twee verschillende methoden om uw wachtwoord opnieuw instellen:</span><span class="sxs-lookup"><span data-stu-id="02319-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="02319-288">**Wachtwoord opnieuw instellen** : Selecteer **dat hun wachtwoord opnieuw instellen van de gebruiker** zodat de gebruiker zelf herstellen als de gebruiker is geregistreerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="02319-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="02319-289">Tijdens de gebruiker van de volgende keer aanmelden, wordt de gebruiker worden vereist voor het oplossen van een challenge multi-factor authentication-server is en vervolgens gedwongen het wachtwoord te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="02319-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="02319-290">Deze optie niet beschikbaar als het gebruikersaccount nog niet is geregistreerd multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="02319-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="02319-291">**Tijdelijke wachtwoord** : Selecteer **genereren van een tijdelijk wachtwoord** onmiddellijk het bestaande wachtwoord ongeldig te maken en het maken van een nieuw tijdelijk wachtwoord voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="02319-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="02319-292">Nieuw tijdelijk wachtwoord verzenden naar een alternatief e-mailadres voor de gebruiker of de manager van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="02319-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="02319-293">Omdat het wachtwoord tijdelijk is, wordt de gebruiker gevraagd het wachtwoord van de aanmeldingspagina te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="02319-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="02319-294">![Beleid](./media/active-directory-identityprotection/1005.png "beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="02319-295">**Opent het dialoogvenster gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="02319-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="02319-296">Op de **Azure AD Identity Protection** blade, klikt u op **gebruikers die zijn gemarkeerd voor risico**.</span><span class="sxs-lookup"><span data-stu-id="02319-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="02319-297">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1006.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="02319-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="02319-298">Selecteer een gebruiker met ten minste één risicogebeurtenissen uit de lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02319-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="02319-299">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1007.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="02319-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="02319-300">Klik op de blade gebruiker **wachtwoord opnieuw instellen**.</span><span class="sxs-lookup"><span data-stu-id="02319-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="02319-301">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1008.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="02319-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="02319-302">Gebruiker risico beveiligingsbeleid</span><span class="sxs-lookup"><span data-stu-id="02319-302">User risk security policy</span></span>
<span data-ttu-id="02319-303">Een beveiligingsbeleid voor gebruiker risico is een beleid voor voorwaardelijke toegang dat het risiconiveau aan een specifieke gebruiker wordt geëvalueerd en herstel en risicobeperking op basis van vooraf gedefinieerde voorwaarden en regels maatregelen.</span><span class="sxs-lookup"><span data-stu-id="02319-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="02319-304">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1009.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="02319-305">Azure AD Identity Protection helpt bij het beheren van de risicobeperking en het doorvoeren van gebruikers die zijn gemarkeerd voor risico doordat u:</span><span class="sxs-lookup"><span data-stu-id="02319-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="02319-306">Stel de gebruikers en groepen die het beleid van toepassing:</span><span class="sxs-lookup"><span data-stu-id="02319-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="02319-307">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1010.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="02319-308">Stel de gebruiker risico niveau drempelwaarde (laag, Gemiddeld of hoog) waarmee het beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="02319-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="02319-309">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1011.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="02319-310">Stel de besturingselementen om te worden afgedwongen wanneer het beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="02319-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="02319-311">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1012.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="02319-312">De status van uw beleid switch:</span><span class="sxs-lookup"><span data-stu-id="02319-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="02319-313">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/403.png "registratieprocedure voor MFA")</span><span class="sxs-lookup"><span data-stu-id="02319-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="02319-314">Bekijken en evalueren van de gevolgen van een wijziging voordat u deze activeert:</span><span class="sxs-lookup"><span data-stu-id="02319-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="02319-315">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1013.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="02319-316">U kiest een **hoge** drempelwaarde vermindert het aantal keer dat een beleid wordt geactiveerd en minimaliseert de overlast voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="02319-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="02319-317">Echter, worden uitgesloten **laag** en **gemiddeld** gebruikers die zijn gemarkeerd voor risico's van het beleid, die mogelijk niet beveiligd identiteiten of apparaten die eerder zijn verdachte of bekend is mogelijk onveilig.</span><span class="sxs-lookup"><span data-stu-id="02319-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="02319-318">Bij het instellen van het beleid</span><span class="sxs-lookup"><span data-stu-id="02319-318">When setting the policy,</span></span>

* <span data-ttu-id="02319-319">Voorkomen dat gebruikers die waarschijnlijk voor het genereren van een groot aantal ONWAAR-positieven (ontwikkelaars, beveiligingsanalisten)</span><span class="sxs-lookup"><span data-stu-id="02319-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="02319-320">Gebruikers in landen waar het inschakelen van het beleid is het niet praktisch uitsluiten (bijvoorbeeld geen toegang tot de helpdesk)</span><span class="sxs-lookup"><span data-stu-id="02319-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="02319-321">Gebruik een **hoge** drempelwaarde tijdens de eerste beleid implementeert, of als u uitdagingen die zichtbaar zijn voor eindgebruikers minimaliseert.</span><span class="sxs-lookup"><span data-stu-id="02319-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="02319-322">Gebruik een **laag** drempelwaarde als uw organisatie betere beveiliging vereist.</span><span class="sxs-lookup"><span data-stu-id="02319-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="02319-323">Als u een **laag** drempelwaarde introduceert extra gebruiker aanmelden uitdagingen, maar een hogere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="02319-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="02319-324">De aanbevolen standaardwaarde voor de meeste organisaties is het configureren van een regel voor een **gemiddeld** drempelwaarde een evenwicht tot stand tussen bruikbaarheid en veiligheid.</span><span class="sxs-lookup"><span data-stu-id="02319-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="02319-325">Zie voor een overzicht van de gerelateerde gebruikerservaring:</span><span class="sxs-lookup"><span data-stu-id="02319-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="02319-326">[Account recovery stroom geknoeid](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="02319-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="02319-327">[Account geblokkeerd stroom geknoeid](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="02319-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="02319-328">**Opent het dialoogvenster gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="02319-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="02319-329">Op de **Azure AD Identity Protection** blade in de **configureren** sectie, klikt u op **risico gebruikersbeleid**.</span><span class="sxs-lookup"><span data-stu-id="02319-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="02319-330">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1009.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="02319-331">Beperkende gebruiker risico 's</span><span class="sxs-lookup"><span data-stu-id="02319-331">Mitigating user risk events</span></span>
<span data-ttu-id="02319-332">Beheerders kunnen een beveiligingsbeleid voor gebruiker risico voorkomen dat gebruikers bij het aanmelden, afhankelijk van het risiconiveau instellen.</span><span class="sxs-lookup"><span data-stu-id="02319-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="02319-333">Een aanmeldingspagina blokkeren:</span><span class="sxs-lookup"><span data-stu-id="02319-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="02319-334">Voorkomt dat het genereren van de nieuwe gebruiker risico's voor de betrokken gebruiker</span><span class="sxs-lookup"><span data-stu-id="02319-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="02319-335">Hiermee kunnen beheerders handmatig herstellen van de risicogebeurtenissen die invloed hebben op de identiteit van de gebruiker en herstellen naar een beveiligde status</span><span class="sxs-lookup"><span data-stu-id="02319-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="02319-336">Registratiebeleid voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="02319-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="02319-337">Azure multi-factor authentication-server is een methode om te controleren wie u bent die het gebruik van meer dan alleen een gebruikersnaam en wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="02319-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="02319-338">Het biedt een tweede beveiligingslaag op gebruikersaanmeldingen en transacties.</span><span class="sxs-lookup"><span data-stu-id="02319-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="02319-339">We raden u aan Azure multi-factor authentication-server voor de gebruikersaanmeldingen omdat deze:</span><span class="sxs-lookup"><span data-stu-id="02319-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="02319-340">Biedt geavanceerde verificatie met een bereik van eenvoudige verificatie-opties</span><span class="sxs-lookup"><span data-stu-id="02319-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="02319-341">Speelt een belangrijke rol bij het voorbereiden van uw organisatie te beveiligen en herstellen van account compromissen</span><span class="sxs-lookup"><span data-stu-id="02319-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="02319-342">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1019.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="02319-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="02319-343">Zie voor meer informatie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="02319-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="02319-344">Azure AD Identity Protection helpt u de uitrollen van multi-factor authentication-registratie beheren door een beleid waarmee u kunt configureren:</span><span class="sxs-lookup"><span data-stu-id="02319-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="02319-345">Stel de gebruikers en groepen die het beleid van toepassing:</span><span class="sxs-lookup"><span data-stu-id="02319-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="02319-346">![MFA-beleid](./media/active-directory-identityprotection/1020.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="02319-347">Stel de instellingen moeten worden afgedwongen wanneer het beleid wordt geactiveerd::</span><span class="sxs-lookup"><span data-stu-id="02319-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="02319-348">![MFA-beleid](./media/active-directory-identityprotection/1021.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="02319-349">De status van uw beleid switch:</span><span class="sxs-lookup"><span data-stu-id="02319-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="02319-350">![MFA-beleid](./media/active-directory-identityprotection/403.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="02319-351">De registratiestatus van de huidige weergave:</span><span class="sxs-lookup"><span data-stu-id="02319-351">View the current registration status:</span></span>

    <span data-ttu-id="02319-352">![MFA-beleid](./media/active-directory-identityprotection/1022.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="02319-353">Zie voor een overzicht van de gerelateerde gebruikerservaring:</span><span class="sxs-lookup"><span data-stu-id="02319-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="02319-354">[Registratie voor meervoudige authenticatiestroom](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="02319-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="02319-355">[Aanmelden-ervaringen met Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="02319-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="02319-356">**Opent het dialoogvenster gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="02319-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="02319-357">Op de **Azure AD Identity Protection** blade in de **configureren** sectie, klikt u op **multi-factor authentication-registratie**.</span><span class="sxs-lookup"><span data-stu-id="02319-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="02319-358">![MFA-beleid](./media/active-directory-identityprotection/1019.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="02319-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="02319-359">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02319-359">Next steps</span></span>
* [<span data-ttu-id="02319-360">Channel 9: Azure AD en Identity weergeven: Identity Protection Preview</span><span class="sxs-lookup"><span data-stu-id="02319-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="02319-361">Inschakelen van beveiliging voor Azure Active Directory-identiteit</span><span class="sxs-lookup"><span data-stu-id="02319-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="02319-362">Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="02319-363">Azure Active Directory-risicogebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="02319-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="02319-364">Azure Active Directory: Identity Protection-meldingen</span><span class="sxs-lookup"><span data-stu-id="02319-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="02319-365">Playbook voor Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="02319-366">Azure Active Directory: Identity Protection verklarende woordenlijst</span><span class="sxs-lookup"><span data-stu-id="02319-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="02319-367">Aanmelden-ervaring met Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="02319-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="02319-368">Azure Active Directory: Identity Protection - blokkering opheffen van gebruikers</span><span class="sxs-lookup"><span data-stu-id="02319-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="02319-369">Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="02319-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
