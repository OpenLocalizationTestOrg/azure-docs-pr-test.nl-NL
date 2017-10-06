---
title: 'Active Directory: Identity Protection aaaAzure | Microsoft Docs'
description: Meer informatie over hoe Azure AD Identity Protection kunt u toolimit Hallo mogelijkheid van een aanvaller tooexploit de identiteit van een verdachte of apparaat en toosecure een identiteit of een apparaat dat eerder verdachte of bekende toobe aangetast.
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
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="e106f-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e106f-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="e106f-105">Azure Active Directory: Identity Protection is een functie van Azure AD Premium-P2 Hallo edition waarmee u kunt:</span><span class="sxs-lookup"><span data-stu-id="e106f-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="e106f-106">Detecteren van mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie</span><span class="sxs-lookup"><span data-stu-id="e106f-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="e106f-107">Automatische antwoorden toodetected verdachte acties die van de organisatie van de gerelateerde tooyour identiteiten configureren</span><span class="sxs-lookup"><span data-stu-id="e106f-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="e106f-108">Verdachte incidenten onderzoeken en tooresolve passende maatregelen nemen ze</span><span class="sxs-lookup"><span data-stu-id="e106f-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="e106f-109">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="e106f-109">Getting started</span></span>

<span data-ttu-id="e106f-110">Microsoft beveiligt cloud-gebaseerde identiteiten voor meer dan een tien jaar.</span><span class="sxs-lookup"><span data-stu-id="e106f-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="e106f-111">Met Azure Active Directory: Identity Protection in uw omgeving, kunt u Hallo toosecure identiteiten maakt gebruik van dezelfde systemen ter bescherming van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e106f-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="e106f-112">Hallo overgrote deel van de beveiliging schendingen nemen plaatsen wanneer aanvallers toegang tooan omgeving krijgen door de identiteit van een gebruiker te stelen.</span><span class="sxs-lookup"><span data-stu-id="e106f-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="e106f-113">Hallo jaar zijn aanvallers steeds effectief gebruik van schendingen van derden en het gebruik van geavanceerde phishingaanvallen geworden.</span><span class="sxs-lookup"><span data-stu-id="e106f-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="e106f-114">Als een aanvaller toegang tooeven gebruikersaccounts met lage bevoegdheden heeft, is het relatief gemakkelijk toe toogain toegang tooimportant bedrijfsbronnen via laterale verplaatsing.</span><span class="sxs-lookup"><span data-stu-id="e106f-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="e106f-115">Als gevolg hiervan moet u:</span><span class="sxs-lookup"><span data-stu-id="e106f-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="e106f-116">Beveiligen van alle identiteiten ongeacht hun machtigingsniveau</span><span class="sxs-lookup"><span data-stu-id="e106f-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="e106f-117">Proactief te voorkomen dat waarmee is geknoeid identiteiten geschonden</span><span class="sxs-lookup"><span data-stu-id="e106f-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="e106f-118">Detectie van verdachte identiteiten is geen eenvoudige taak.</span><span class="sxs-lookup"><span data-stu-id="e106f-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="e106f-119">Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect afwijkingen en verdachte incidenten die mogelijk aangeven identiteiten waarmee is geknoeid.</span><span class="sxs-lookup"><span data-stu-id="e106f-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="e106f-120">Met deze gegevens Identity Protection genereert rapporten en meldingen waarmee u tooevaluate Hallo heeft problemen gedetecteerd en het juiste risicobeperking of herstelacties duren.</span><span class="sxs-lookup"><span data-stu-id="e106f-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="e106f-121">Azure Active Directory: Identity Protection is meer dan een controle en rapportage.</span><span class="sxs-lookup"><span data-stu-id="e106f-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="e106f-122">tooprotect identiteiten van uw organisatie, kunt u risico-beleidsregels die automatisch toodetected problemen reageren als een opgegeven risiconiveau is bereikt.</span><span class="sxs-lookup"><span data-stu-id="e106f-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="e106f-123">Deze beleidsregels bovendien tooother voorwaardelijke toegang tot de besturingselementen die worden geleverd door Azure Active Directory en EMS, kunnen automatisch blokkeren of initiëren adaptieve herstelacties met inbegrip van wachtwoorden en afdwingen van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="e106f-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="e106f-124">Mogelijkheden voor preventie van identiteit</span><span class="sxs-lookup"><span data-stu-id="e106f-124">Identity Protection capabilities</span></span>

<span data-ttu-id="e106f-125">**Detecteren van zwakke plekken en riskant accounts:**</span><span class="sxs-lookup"><span data-stu-id="e106f-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="e106f-126">Aangepaste aanbevelingen tooimprove bieden algehele beveiligingsstatus beveiligingslekken markeert</span><span class="sxs-lookup"><span data-stu-id="e106f-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="e106f-127">Aanmelden risiconiveaus berekenen</span><span class="sxs-lookup"><span data-stu-id="e106f-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="e106f-128">Gebruiker risiconiveaus berekenen</span><span class="sxs-lookup"><span data-stu-id="e106f-128">Calculating user risk levels</span></span>


<span data-ttu-id="e106f-129">**Bezig met het onderzoeken van risico's:**</span><span class="sxs-lookup"><span data-stu-id="e106f-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="e106f-130">Verzenden van meldingen voor risico 's</span><span class="sxs-lookup"><span data-stu-id="e106f-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="e106f-131">Het onderzoeken van risico's met behulp van de relevante en contextuele informatie</span><span class="sxs-lookup"><span data-stu-id="e106f-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="e106f-132">Biedt eenvoudige werkstromen tootrack onderzoeken</span><span class="sxs-lookup"><span data-stu-id="e106f-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="e106f-133">Eenvoudige toegang bieden tooremediation acties zoals het wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e106f-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="e106f-134">**Beleid voor voorwaardelijke toegang op basis van risico's:**</span><span class="sxs-lookup"><span data-stu-id="e106f-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="e106f-135">Beleid toomitigate riskant aanmeldingen door aanmeldingen blokkeren of uitdagingen voor meervoudige verificatie vereisen.</span><span class="sxs-lookup"><span data-stu-id="e106f-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="e106f-136">Beleid tooblock of beveiligde riskant gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="e106f-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="e106f-137">Beleid toorequire gebruikers tooregister voor multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="e106f-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="e106f-138">Identity Protection-functies</span><span class="sxs-lookup"><span data-stu-id="e106f-138">Identity Protection roles</span></span>

<span data-ttu-id="e106f-139">tooload saldo Hallo beheeractiviteiten rond de Identity Protection-implementatie, kunt u verschillende rollen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="e106f-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="e106f-140">Azure AD Identity Protection ondersteunt 3 directory-functies:</span><span class="sxs-lookup"><span data-stu-id="e106f-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="e106f-141">Rol</span><span class="sxs-lookup"><span data-stu-id="e106f-141">Role</span></span>                         | <span data-ttu-id="e106f-142">Kan doen</span><span class="sxs-lookup"><span data-stu-id="e106f-142">Can do</span></span>                          | <span data-ttu-id="e106f-143">Is niet mogelijk</span><span class="sxs-lookup"><span data-stu-id="e106f-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="e106f-144">Globale beheerder</span><span class="sxs-lookup"><span data-stu-id="e106f-144">Global administrator</span></span>         | <span data-ttu-id="e106f-145">Volledige toegang tooIdentity, beveiliging, vrijgeven Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e106f-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="e106f-146">Beveiligingsbeheerder</span><span class="sxs-lookup"><span data-stu-id="e106f-146">Security administrator</span></span>       | <span data-ttu-id="e106f-147">Volledige toegang tooIdentity beveiliging</span><span class="sxs-lookup"><span data-stu-id="e106f-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="e106f-148">Ingebouwde Identity Protection, wachtwoorden opnieuw instellen voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="e106f-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="e106f-149">Beveiligingslezer</span><span class="sxs-lookup"><span data-stu-id="e106f-149">Security reader</span></span>              | <span data-ttu-id="e106f-150">Klaar voor alleen-lezen toegang tooIdentity beveiliging</span><span class="sxs-lookup"><span data-stu-id="e106f-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="e106f-151">Ingebouwde Identity Protection, remidiate gebruikers,-beleid configureren, wachtwoorden opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e106f-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="e106f-152">Zie voor meer informatie [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e106f-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="e106f-153">Detectie</span><span class="sxs-lookup"><span data-stu-id="e106f-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="e106f-154">Beveiligingsproblemen</span><span class="sxs-lookup"><span data-stu-id="e106f-154">Vulnerabilities</span></span>

<span data-ttu-id="e106f-155">Azure Active Directory: Identity Protection analyses van uw configuratie en beveiligingsproblemen die invloed op uw gebruikers-id's hebben kunnen detecteert.</span><span class="sxs-lookup"><span data-stu-id="e106f-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="e106f-156">Zie voor meer informatie [beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="e106f-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="e106f-157">Risico 's</span><span class="sxs-lookup"><span data-stu-id="e106f-157">Risk events</span></span>

<span data-ttu-id="e106f-158">Azure Active Directory maakt gebruik van geavanceerde machine learning-algoritmen en methodiek toodetect verdachte acties die gerelateerd tooyour gebruikersidentiteiten zijn.</span><span class="sxs-lookup"><span data-stu-id="e106f-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="e106f-159">Hallo system maakt een record voor elke gedetecteerde verdachte actie.</span><span class="sxs-lookup"><span data-stu-id="e106f-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="e106f-160">Deze records worden ook wel bekend als risico's.</span><span class="sxs-lookup"><span data-stu-id="e106f-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="e106f-161">Zie [Risicogebeurtenissen in Azure Active Directory](active-directory-identity-protection-risk-events.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e106f-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="e106f-162">Onderzoek</span><span class="sxs-lookup"><span data-stu-id="e106f-162">Investigation</span></span>
<span data-ttu-id="e106f-163">Uw reis door Identity Protection begint meestal met Hallo Identity Protection-dashboard.</span><span class="sxs-lookup"><span data-stu-id="e106f-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="e106f-164">![Herstel](./media/active-directory-identityprotection/1000.png "herstel")</span><span class="sxs-lookup"><span data-stu-id="e106f-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="e106f-165">Hallo-dashboard hebt u toegang hebt tot:</span><span class="sxs-lookup"><span data-stu-id="e106f-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="e106f-166">Rapporten, zoals **gebruikers die zijn gemarkeerd voor risico**, **bestaat de kans dat gebeurtenissen** en **beveiligingsproblemen**</span><span class="sxs-lookup"><span data-stu-id="e106f-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="e106f-167">Instellingen zoals Hallo configuratie van uw **beveiligingsbeleid**, **meldingen** en **multi-factor authentication-registratie**</span><span class="sxs-lookup"><span data-stu-id="e106f-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="e106f-168">Het is doorgaans het startpunt voor onderzoek, waardoor het Hallo-proces controleren Hallo activiteiten, logboeken en andere relevante informatie gerelateerde tooa risico gebeurtenis toodecide of herstel of afname stappen zijn nodig is, en hoe Hallo identiteit was geknoeid en begrijpen hoe Hallo geknoeid met de identiteit is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e106f-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="e106f-169">U kunt verbinden, uw onderzoek activiteiten toohello [meldingen](active-directory-identityprotection-notifications.md) Azure Active Directory Protection per e-mail verzendt.</span><span class="sxs-lookup"><span data-stu-id="e106f-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="e106f-170">Hallo volgende secties vindt u meer details en Hallo stappen die gerelateerd tooan onderzoek zijn.</span><span class="sxs-lookup"><span data-stu-id="e106f-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="e106f-171">Riskant aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="e106f-171">Risky sign-ins</span></span>

<span data-ttu-id="e106f-172">Azure Active Directory detecteert [risico gebeurtenistypen](active-directory-reporting-risk-events.md#risk-event-types) in realtime en offline.</span><span class="sxs-lookup"><span data-stu-id="e106f-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="e106f-173">Elke risicogebeurtenis dat is aangetroffen voor een aanmelding van een gebruiker bijdraagt tooa logisch concept is aangeroepen riskant aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e106f-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="e106f-174">Een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk niet uitgevoerd door Hallo rechtmatige eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="e106f-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="e106f-175">Aanmelden risiconiveau</span><span class="sxs-lookup"><span data-stu-id="e106f-175">Sign-in risk level</span></span>

<span data-ttu-id="e106f-176">Een aanmeldingspagina risiconiveau geeft aan dat er (hoog, Gemiddeld of laag) Hallo kans een aanmeldingspoging is niet uitgevoerd door Hallo legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="e106f-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="e106f-177">Beperkende aanmelden risico 's</span><span class="sxs-lookup"><span data-stu-id="e106f-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="e106f-178">Een beperking is een actie toolimit Hallo mogelijkheid van een aanvaller tooexploit een waarmee is geknoeid identiteit of het apparaat zonder herstelstatus Hallo identiteit of het apparaat tooa veilig.</span><span class="sxs-lookup"><span data-stu-id="e106f-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="e106f-179">Een risicobeperking vorige aanmelden risicogebeurtenissen die zijn gekoppeld aan het Hallo-identiteit of het apparaat niet is opgelost.</span><span class="sxs-lookup"><span data-stu-id="e106f-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="e106f-180">toomitigate riskant aanmeldingen automatisch, kunt u aanmelden risico beveiliging policicies configureren.</span><span class="sxs-lookup"><span data-stu-id="e106f-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="e106f-181">Met deze beleidsregels, u Overweeg Hallo risiconiveau van Hallo gebruiker of Hallo aanmelden tooblock riskant aanmeldingen of Hallo gebruiker tooperform meervoudige authenticatie.</span><span class="sxs-lookup"><span data-stu-id="e106f-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="e106f-182">Deze acties kunnen voorkomen dat een aanvaller een gestolen identiteit toocause schade misbruik van, en mogelijk hebt u een bepaalde tijd toosecure Hallo identiteit.</span><span class="sxs-lookup"><span data-stu-id="e106f-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="e106f-183">Beveiligingsbeleid Aanmelden risico</span><span class="sxs-lookup"><span data-stu-id="e106f-183">Sign-in risk security policy</span></span>
<span data-ttu-id="e106f-184">Een beleid voor aanmelden risico is een beleid voor voorwaardelijke toegang dat Hallo risico tooa specifieke aanmelden wordt geëvalueerd en oplossingen op basis van vooraf gedefinieerde voorwaarden en regels van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="e106f-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="e106f-185">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1014.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="e106f-186">Azure AD Identity Protection helpt u Hallo risicobeperking van riskante aanmeldingen doordat u beheren:</span><span class="sxs-lookup"><span data-stu-id="e106f-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="e106f-187">Set Hallo gebruikers en groepen Hallo beleid van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="e106f-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="e106f-188">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1015.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="e106f-189">Hallo aanmelden risico niveau drempel instellen (laag, Gemiddeld of hoog) waarmee de Hallo beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="e106f-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="e106f-190">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1016.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="e106f-191">Set Hallo besturingselementen toobe afgedwongen als het Hallo-beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="e106f-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="e106f-192">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1017.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="e106f-193">Hallo-status van uw beleid switch:</span><span class="sxs-lookup"><span data-stu-id="e106f-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="e106f-194">![Registratieprocedure voor MFA](./media/active-directory-identityprotection/403.png "registratieprocedure voor MFA")</span><span class="sxs-lookup"><span data-stu-id="e106f-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="e106f-195">Bekijken en evalueren Hallo gevolgen van een wijziging voordat u deze activeert:</span><span class="sxs-lookup"><span data-stu-id="e106f-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="e106f-196">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1018.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="e106f-197">Wat u nodig hebt tooknow</span><span class="sxs-lookup"><span data-stu-id="e106f-197">What you need tooknow</span></span>
<span data-ttu-id="e106f-198">U kunt een aanmeldingspagina risico beveiliging beleid toorequire multi-factor authentication configureren:</span><span class="sxs-lookup"><span data-stu-id="e106f-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="e106f-199">![Beleid voor aanmelden risico](./media/active-directory-identityprotection/1017.png "aanmelden risico beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="e106f-200">Echter, uit veiligheidsoverwegingen deze instelling werkt alleen voor gebruikers die al zijn geregistreerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="e106f-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="e106f-201">Als Hallo voorwaarde toorequire meervoudige verificatie voor een gebruiker die nog niet is geregistreerd voor multi-factor authentication is voldaan, is Hallo gebruiker geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e106f-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="e106f-202">Als het wordt aanbevolen als u wilt dat toorequire multi-factor authentication voor riskante aanmeldingen, moet u:</span><span class="sxs-lookup"><span data-stu-id="e106f-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="e106f-203">Hallo inschakelen [registratiebeleid multi-factorauthenticatie](#multi-factor-authentication-registration-policy) voor Hallo van invloed op gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e106f-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="e106f-204">Hallo toologin gebruikers in een niet-riskant sessie tooperform invloed op een registratieprocedure voor MFA vereisen</span><span class="sxs-lookup"><span data-stu-id="e106f-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="e106f-205">U deze stappen uitvoert, zorgt u ervoor dat meervoudige verificatie is vereist voor een riskante aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e106f-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="e106f-206">Aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="e106f-206">Best practices</span></span>
<span data-ttu-id="e106f-207">U kiest een **hoge** drempelwaarde vermindert het aantal keren dat een beleid wordt geactiveerd en minimaliseert Hallo impact toousers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e106f-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="e106f-208">Echter, worden uitgesloten **laag** en **gemiddeld** aanmeldingen gemarkeerd voor kwetsbaar voor aanvallen via Hallo-beleid, dat een aanvaller gebruikmaakt van de identiteit van een verdachte kan niet worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="e106f-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="e106f-209">Wanneer de instelling beleid Hallo</span><span class="sxs-lookup"><span data-stu-id="e106f-209">When setting hello policy,</span></span>

* <span data-ttu-id="e106f-210">Gebruikers die geen / multi-factor authentication-server kunnen geen uitsluiten</span><span class="sxs-lookup"><span data-stu-id="e106f-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="e106f-211">Gebruikers in landen waar inschakelen Hallo beleid is het niet praktisch uitsluiten (bijvoorbeeld geen toohelpdesk toegang)</span><span class="sxs-lookup"><span data-stu-id="e106f-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="e106f-212">Voorkomen dat gebruikers die waarschijnlijk toogenerate veel ONWAAR-positieven (ontwikkelaars, beveiligingsanalisten zijn)</span><span class="sxs-lookup"><span data-stu-id="e106f-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="e106f-213">Gebruik een **hoge** drempelwaarde tijdens de eerste beleid implementeert, of als u uitdagingen die zichtbaar zijn voor eindgebruikers minimaliseert.</span><span class="sxs-lookup"><span data-stu-id="e106f-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="e106f-214">Gebruik een **laag** drempelwaarde als uw organisatie betere beveiliging vereist.</span><span class="sxs-lookup"><span data-stu-id="e106f-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="e106f-215">Als u een **laag** drempelwaarde introduceert extra gebruiker aanmelden uitdagingen, maar een hogere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="e106f-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="e106f-216">Hallo standaard aanbevolen voor de meeste organisaties tooconfigure is een regel voor een **gemiddeld** drempelwaarde toostrike een balans tussen bruikbaarheid en veiligheid.</span><span class="sxs-lookup"><span data-stu-id="e106f-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="e106f-217">Hallo aanmelden risico beleid is:</span><span class="sxs-lookup"><span data-stu-id="e106f-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="e106f-218">Toegepaste tooall browserverkeer en aanmeldingen die moderne authenticatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e106f-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="e106f-219">Niet toegepast tooapplications met oudere-protocollen door Hallo WS-Trust-eindpunt op Hallo federatieve IDP, zoals ADFS uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="e106f-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="e106f-220">Hallo **Risicogebeurtenissen** worden alle gebeurtenissen op deze pagina in Hallo Identity Protection-console:</span><span class="sxs-lookup"><span data-stu-id="e106f-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="e106f-221">Dit beleid is toegepast</span><span class="sxs-lookup"><span data-stu-id="e106f-221">This policy was applied to</span></span>
* <span data-ttu-id="e106f-222">U kunt Hallo activiteiten controleren en bepalen of de actie Hallo juiste of niet is</span><span class="sxs-lookup"><span data-stu-id="e106f-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="e106f-223">Voor een overzicht van Hallo gerelateerde gebruikerservaring, Zie:</span><span class="sxs-lookup"><span data-stu-id="e106f-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="e106f-224">Herstel voor riskante aanmelden</span><span class="sxs-lookup"><span data-stu-id="e106f-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="e106f-225">Riskant aanmelden geblokkeerd</span><span class="sxs-lookup"><span data-stu-id="e106f-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="e106f-226">Aanmelden-ervaring met Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e106f-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="e106f-227">**dialoogvenster tooopen Hallo-gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="e106f-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="e106f-228">Op Hallo **Azure AD Identity Protection** blade in Hallo **configureren** sectie, klikt u op **aanmelden risico beleid**.</span><span class="sxs-lookup"><span data-stu-id="e106f-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="e106f-229">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1014.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="e106f-230">Gebruikers voor wie wordt aangegeven dat ze risico lopen</span><span class="sxs-lookup"><span data-stu-id="e106f-230">Users flagged for risk</span></span>

<span data-ttu-id="e106f-231">Alle actieve [bestaat de kans dat gebeurtenissen](active-directory-identity-protection-risk-events.md) die zijn gedetecteerd door Azure Active Directory voor een gebruiker bijdragen tooa logisch concept is aangeroepen gebruiker risico.</span><span class="sxs-lookup"><span data-stu-id="e106f-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="e106f-232">Een gebruiker die is gemarkeerd voor risico is een indicator voor een gebruikersaccount die mogelijk zijn aangetast.</span><span class="sxs-lookup"><span data-stu-id="e106f-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Gebruikers voor wie wordt aangegeven dat ze risico lopen](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="e106f-234">Risiconiveau van gebruiker</span><span class="sxs-lookup"><span data-stu-id="e106f-234">User risk level</span></span>

<span data-ttu-id="e106f-235">Het risiconiveau van een gebruiker wordt aangegeven (hoog, Gemiddeld of laag) van de kans op Hallo Hallo gebruikersidentiteit is aangetast.</span><span class="sxs-lookup"><span data-stu-id="e106f-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="e106f-236">Deze wordt berekend op basis van Hallo gebruiker risico's die gekoppeld aan de identiteit van een gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="e106f-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="e106f-237">Hallo status van een risicogebeurtenis is een **Active** of **gesloten**.</span><span class="sxs-lookup"><span data-stu-id="e106f-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="e106f-238">Alleen het risico van gebeurtenissen die zijn **Active** bijdragen toohello gebruiker risico niveau berekening.</span><span class="sxs-lookup"><span data-stu-id="e106f-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="e106f-239">Hallo gebruiker risiconiveau wordt berekend met behulp van Hallo invoer te volgen:</span><span class="sxs-lookup"><span data-stu-id="e106f-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="e106f-240">Actieve risicogebeurtenissen die invloed hebben op Hallo-gebruiker</span><span class="sxs-lookup"><span data-stu-id="e106f-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="e106f-241">Risiconiveau van deze gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="e106f-241">Risk level of these events</span></span>
* <span data-ttu-id="e106f-242">Hiermee wordt aangegeven of welke herstelacties zijn gemaakt</span><span class="sxs-lookup"><span data-stu-id="e106f-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="e106f-243">![Gebruiker risico's](./media/active-directory-identityprotection/1031.png "gebruiker risico's")</span><span class="sxs-lookup"><span data-stu-id="e106f-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="e106f-244">U kunt gebruiken Hallo gebruiker risico niveaus toocreate beleidsregels voor voorwaardelijke toegang die riskant gebruikers aanmelden blokkeren, of zorgen dat ze toosecurely hun wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e106f-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="e106f-245">Risico's handmatig sluiten</span><span class="sxs-lookup"><span data-stu-id="e106f-245">Closing risk events manually</span></span>

<span data-ttu-id="e106f-246">In de meeste gevallen wordt u herstelacties uitvoeren, zoals een beveiligd wachtwoord opnieuw instellen van tooautomatically sluiten risico's.</span><span class="sxs-lookup"><span data-stu-id="e106f-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="e106f-247">Echter, dit mogelijk niet altijd mogelijk.</span><span class="sxs-lookup"><span data-stu-id="e106f-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="e106f-248">Dit is, bijvoorbeeld Hallo geval, wanneer:</span><span class="sxs-lookup"><span data-stu-id="e106f-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="e106f-249">Een gebruiker met actieve risicogebeurtenissen is verwijderd</span><span class="sxs-lookup"><span data-stu-id="e106f-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="e106f-250">Een onderzoek blijkt dat een risicogebeurtenis gemelde heeft zijn uitvoeren door Hallo legitieme gebruiker</span><span class="sxs-lookup"><span data-stu-id="e106f-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="e106f-251">Omdat de risico's die zijn **Active** bijdragen toohello gebruiker risico berekening, moet u wellicht toomanually een risiconiveau verlagen door het risico's handmatig te sluiten.</span><span class="sxs-lookup"><span data-stu-id="e106f-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="e106f-252">In de loop van de Hallo van onderzoek, kunt u een van deze acties toochange Hallo status van een risicogebeurtenis tootake kiezen:</span><span class="sxs-lookup"><span data-stu-id="e106f-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="e106f-253">![Acties](./media/active-directory-identityprotection/34.png "acties")</span><span class="sxs-lookup"><span data-stu-id="e106f-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="e106f-254">**Los** - als na een risicogebeurtenis onderzoeken, u een juiste herstelactie buiten Identity Protection heeft ondernomen, en u van mening dat risico Hallo gebeurtenis overwogen worden gesloten bent, Hallo-gebeurtenis markeren als opgelost.</span><span class="sxs-lookup"><span data-stu-id="e106f-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="e106f-255">Opgelost gebeurtenissen Hallo risico's van de gebeurtenis status tooClosed wordt ingesteld en Hallo risicogebeurtenis wordt niet langer bijdragen toouser risico.</span><span class="sxs-lookup"><span data-stu-id="e106f-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="e106f-256">**Markeren als fout-positieve** -In sommige gevallen kan u een risicogebeurtenis onderzoeken en onjuist is gemarkeerd als een riskante te detecteren.</span><span class="sxs-lookup"><span data-stu-id="e106f-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="e106f-257">Kunt u beperken Hallo aantal dergelijke instanties door Hallo risicogebeurtenis als fout-positieve markeren.</span><span class="sxs-lookup"><span data-stu-id="e106f-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="e106f-258">Dit helpt Hallo machine learning-algoritmen tooimprove Hallo classificatie van soortgelijke gebeurtenissen in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="e106f-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="e106f-259">Hallo-status van de fout-positieve gebeurtenissen is te**gesloten** en ze worden niet meer bij te dragen toouser risico.</span><span class="sxs-lookup"><span data-stu-id="e106f-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="e106f-260">**Negeren** : als u een herstelactie niet hebt gemaakt, maar wilt Hallo risico gebeurtenis toobe verwijderd uit de actieve lijst hello, kunt u een risicogebeurtenis negeren markeren en Hallo gebeurtenisstatus worden gesloten.</span><span class="sxs-lookup"><span data-stu-id="e106f-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="e106f-261">Genegeerd gebeurtenissen bijdragen niet toouser risico.</span><span class="sxs-lookup"><span data-stu-id="e106f-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="e106f-262">Deze optie dient alleen ongebruikelijke omstandigheden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e106f-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="e106f-263">**Opnieuw activeren** -gebeurtenissen die handmatig zijn gesloten risico (door te kiezen **los**, **fout-positief**, of **negeren**) kan opnieuw worden geactiveerd, Hallo instellen om de gebeurtenisstatus weer te**Active**.</span><span class="sxs-lookup"><span data-stu-id="e106f-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="e106f-264">Opnieuw geactiveerde risicogebeurtenissen bijdragen toohello gebruiker risico niveau berekening.</span><span class="sxs-lookup"><span data-stu-id="e106f-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="e106f-265">Risico's gesloten via herstel (zoals een beveiligd wachtwoord opnieuw instellen) kunnen niet opnieuw worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e106f-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="e106f-266">**dialoogvenster tooopen Hallo-gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="e106f-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="e106f-267">Op Hallo **Azure AD Identity Protection** blade onder **onderzoeken**, klikt u op **bestaat de kans dat gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="e106f-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="e106f-268">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1002.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="e106f-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="e106f-269">In Hallo **bestaat de kans dat gebeurtenissen** lijst, klikt u op een risico.</span><span class="sxs-lookup"><span data-stu-id="e106f-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="e106f-270">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1003.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="e106f-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="e106f-271">Hallo risico blade met de rechtermuisknop op een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e106f-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="e106f-272">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1004.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="e106f-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="e106f-273">Alle gebeurtenissen van de risico's voor een gebruiker sluiten handmatig</span><span class="sxs-lookup"><span data-stu-id="e106f-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="e106f-274">In plaats van handmatig sluiten afzonderlijk risico's voor een gebruiker, biedt Azure Active Directory: Identity Protection u ook een methode tooclose alle gebeurtenissen voor een gebruiker met één klik.</span><span class="sxs-lookup"><span data-stu-id="e106f-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="e106f-275">![Acties](./media/active-directory-identityprotection/2222.png "acties")</span><span class="sxs-lookup"><span data-stu-id="e106f-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="e106f-276">Wanneer u klikt op **sluiten alle gebeurtenissen**, alle gebeurtenissen zijn gesloten en Hallo van invloed op een gebruiker is niet langer risico.</span><span class="sxs-lookup"><span data-stu-id="e106f-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="e106f-277">Beveiligingsstatus gebruiker risico 's</span><span class="sxs-lookup"><span data-stu-id="e106f-277">Remediating user risk events</span></span>

<span data-ttu-id="e106f-278">Een herstel is een actie toosecure een identiteit of een apparaat dat eerder is verdacht of toobe bekend is geknoeid.</span><span class="sxs-lookup"><span data-stu-id="e106f-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="e106f-279">Een herstelactie Hallo identiteit of het apparaat tooa veilige status herstelt en vorige risico's die zijn gekoppeld aan het Hallo-identiteit of het apparaat wordt omgezet.</span><span class="sxs-lookup"><span data-stu-id="e106f-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="e106f-280">tooremediate-gebeurtenissen voor het risico van gebruikers, kunt u:</span><span class="sxs-lookup"><span data-stu-id="e106f-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="e106f-281">Een beveiligd wachtwoord opnieuw instellen van tooremediate gebruiker risicogebeurtenissen handmatig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e106f-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="e106f-282">Configureren van een gebruiker risico beveiliging beleid toomitigate of risicogebeurtenissen gebruiker automatisch herstellen</span><span class="sxs-lookup"><span data-stu-id="e106f-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="e106f-283">Hallo geïnfecteerd apparaat herstellen met installatiekopie</span><span class="sxs-lookup"><span data-stu-id="e106f-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="e106f-284">Handmatige beveiligd wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e106f-284">Manual secure password reset</span></span>
<span data-ttu-id="e106f-285">Een beveiligd wachtwoord opnieuw instellen is een effectieve herstel voor veel risicogebeurtenissen en wanneer uitgevoerd, sluit u deze risicogebeurtenissen automatisch en risiconiveau Hallo-gebruiker opnieuw worden berekend.</span><span class="sxs-lookup"><span data-stu-id="e106f-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="e106f-286">U kunt Hallo Identity Protection-dashboard tooinitiate een wachtwoord opnieuw instellen voor een gebruiker riskant.</span><span class="sxs-lookup"><span data-stu-id="e106f-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="e106f-287">Hallo gerelateerde dialoogvenster bevat twee verschillende methoden tooreset een wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="e106f-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="e106f-288">**Wachtwoord opnieuw instellen** : Selecteer **Hallo gebruiker tooreset hun wachtwoord vereisen** tooallow Hallo gebruiker tooself herstellen als Hallo gebruiker is geregistreerd voor multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="e106f-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="e106f-289">Tijdens het Hallo van de gebruiker volgende aanmelden zijn Hallo gebruiker vereist toosolve is een multi-factor authentication-vraag en vervolgens, de geforceerde toochange Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e106f-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="e106f-290">Deze optie niet beschikbaar als Hallo gebruikersaccount nog niet is geregistreerd multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="e106f-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="e106f-291">**Tijdelijke wachtwoord** : Selecteer **genereren van een tijdelijk wachtwoord** tooimmediately Hallo bestaande wachtwoord ongeldig te maken en een nieuw tijdelijk wachtwoord voor gebruiker Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="e106f-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="e106f-292">Hallo nieuw tijdelijk wachtwoord tooan alternatieve e-mailadres voor Hallo gebruiker of toohello Gebruikersbeheer verzenden.</span><span class="sxs-lookup"><span data-stu-id="e106f-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="e106f-293">Omdat Hallo wachtwoord tijdelijke, Hallo gebruiker worden opgegeven na vragen aan gebruiker toochange Hallo wachtwoord bij aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e106f-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="e106f-294">![Beleid](./media/active-directory-identityprotection/1005.png "beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="e106f-295">**dialoogvenster tooopen Hallo-gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="e106f-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="e106f-296">Op Hallo **Azure AD Identity Protection** blade, klikt u op **gebruikers die zijn gemarkeerd voor risico**.</span><span class="sxs-lookup"><span data-stu-id="e106f-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="e106f-297">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1006.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="e106f-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="e106f-298">Selecteer een gebruiker met ten minste één risicogebeurtenissen in Hallo lijst van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e106f-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="e106f-299">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1007.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="e106f-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="e106f-300">Klik op Hallo gebruiker blade **wachtwoord opnieuw instellen**.</span><span class="sxs-lookup"><span data-stu-id="e106f-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="e106f-301">![Handmatige wachtwoordherstel](./media/active-directory-identityprotection/1008.png "handmatige wachtwoord opnieuw instellen")</span><span class="sxs-lookup"><span data-stu-id="e106f-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="e106f-302">Gebruiker risico beveiligingsbeleid</span><span class="sxs-lookup"><span data-stu-id="e106f-302">User risk security policy</span></span>
<span data-ttu-id="e106f-303">Een beveiligingsbeleid voor gebruiker risico is een beleid voor voorwaardelijke toegang dat Hallo risico niveau tooa specifieke gebruiker wordt geëvalueerd en herstel en risicobeperking op basis van vooraf gedefinieerde voorwaarden en regels maatregelen.</span><span class="sxs-lookup"><span data-stu-id="e106f-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="e106f-304">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1009.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="e106f-305">Azure AD Identity Protection helpt u Hallo risicobeperking en het doorvoeren van gebruikers die zijn gemarkeerd voor risico doordat u beheren:</span><span class="sxs-lookup"><span data-stu-id="e106f-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="e106f-306">Set Hallo gebruikers en groepen Hallo beleid van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="e106f-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="e106f-307">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1010.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="e106f-308">Hallo gebruiker risico niveau drempelwaarde (laag, Gemiddeld of hoog) die Hallo beleid activeert instellen:</span><span class="sxs-lookup"><span data-stu-id="e106f-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="e106f-309">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1011.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="e106f-310">Set Hallo besturingselementen toobe afgedwongen als het Hallo-beleid wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="e106f-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="e106f-311">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1012.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="e106f-312">Hallo-status van uw beleid switch:</span><span class="sxs-lookup"><span data-stu-id="e106f-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="e106f-313">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/403.png "registratieprocedure voor MFA")</span><span class="sxs-lookup"><span data-stu-id="e106f-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="e106f-314">Bekijken en evalueren Hallo gevolgen van een wijziging voordat u deze activeert:</span><span class="sxs-lookup"><span data-stu-id="e106f-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="e106f-315">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1013.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="e106f-316">U kiest een **hoge** drempelwaarde vermindert het aantal keren dat een beleid wordt geactiveerd en minimaliseert Hallo impact toousers Hallo.</span><span class="sxs-lookup"><span data-stu-id="e106f-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="e106f-317">Echter, worden uitgesloten **laag** en **gemiddeld** gebruikers die zijn gemarkeerd voor kwetsbaar voor aanvallen via Hallo-beleid kan niet worden beveiligd identiteiten of apparaten die eerder zijn verdachte of bekend toobe aangetast.</span><span class="sxs-lookup"><span data-stu-id="e106f-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="e106f-318">Wanneer de instelling beleid Hallo</span><span class="sxs-lookup"><span data-stu-id="e106f-318">When setting hello policy,</span></span>

* <span data-ttu-id="e106f-319">Voorkomen dat gebruikers die waarschijnlijk toogenerate veel ONWAAR-positieven (ontwikkelaars, beveiligingsanalisten zijn)</span><span class="sxs-lookup"><span data-stu-id="e106f-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="e106f-320">Gebruikers in landen waar inschakelen Hallo beleid is het niet praktisch uitsluiten (bijvoorbeeld geen toohelpdesk toegang)</span><span class="sxs-lookup"><span data-stu-id="e106f-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="e106f-321">Gebruik een **hoge** drempelwaarde tijdens de eerste beleid implementeert, of als u uitdagingen die zichtbaar zijn voor eindgebruikers minimaliseert.</span><span class="sxs-lookup"><span data-stu-id="e106f-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="e106f-322">Gebruik een **laag** drempelwaarde als uw organisatie betere beveiliging vereist.</span><span class="sxs-lookup"><span data-stu-id="e106f-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="e106f-323">Als u een **laag** drempelwaarde introduceert extra gebruiker aanmelden uitdagingen, maar een hogere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="e106f-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="e106f-324">Hallo standaard aanbevolen voor de meeste organisaties tooconfigure is een regel voor een **gemiddeld** drempelwaarde toostrike een balans tussen bruikbaarheid en veiligheid.</span><span class="sxs-lookup"><span data-stu-id="e106f-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="e106f-325">Voor een overzicht van Hallo gerelateerde gebruikerservaring, Zie:</span><span class="sxs-lookup"><span data-stu-id="e106f-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="e106f-326">[Account recovery stroom geknoeid](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="e106f-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="e106f-327">[Account geblokkeerd stroom geknoeid](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="e106f-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="e106f-328">**dialoogvenster tooopen Hallo-gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="e106f-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="e106f-329">Op Hallo **Azure AD Identity Protection** blade in Hallo **configureren** sectie, klikt u op **risico gebruikersbeleid**.</span><span class="sxs-lookup"><span data-stu-id="e106f-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="e106f-330">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1009.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="e106f-331">Beperkende gebruiker risico 's</span><span class="sxs-lookup"><span data-stu-id="e106f-331">Mitigating user risk events</span></span>
<span data-ttu-id="e106f-332">Beheerders kunnen een gebruiker risico beveiliging beleid tooblock gebruikers bij het aanmelden, afhankelijk van het risiconiveau Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="e106f-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="e106f-333">Een aanmeldingspagina blokkeren:</span><span class="sxs-lookup"><span data-stu-id="e106f-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="e106f-334">Voorkomt dat Hallo genereren van de nieuwe gebruiker risicogebeurtenissen voor Hallo van invloed op een gebruiker</span><span class="sxs-lookup"><span data-stu-id="e106f-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="e106f-335">Hiermee beheerders toomanually hello risicogebeurtenissen die invloed hebben op Hallo gebruikersidentiteit herstellen en herstel hem tooa beveiligde status</span><span class="sxs-lookup"><span data-stu-id="e106f-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="e106f-336">Registratiebeleid voor meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="e106f-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="e106f-337">Azure multi-factor authentication-server is een methode om te controleren wie u bent die Hallo gebruik van meer dan alleen een gebruikersnaam en wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="e106f-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="e106f-338">Het biedt een tweede beveiligingslaag beveiliging toouser aanmeldingen en transacties.</span><span class="sxs-lookup"><span data-stu-id="e106f-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="e106f-339">We raden u aan Azure multi-factor authentication-server voor de gebruikersaanmeldingen omdat deze:</span><span class="sxs-lookup"><span data-stu-id="e106f-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="e106f-340">Biedt geavanceerde verificatie met een bereik van eenvoudige verificatie-opties</span><span class="sxs-lookup"><span data-stu-id="e106f-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="e106f-341">Speelt een belangrijke rol bij het voorbereiden van uw organisatie tooprotect en herstellen van account compromissen</span><span class="sxs-lookup"><span data-stu-id="e106f-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="e106f-342">![Gebruikersbeleid ridk](./media/active-directory-identityprotection/1019.png "ridk gebruikersbeleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="e106f-343">Zie voor meer informatie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e106f-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="e106f-344">Azure AD Identity Protection helpt u Hallo uitrollen van multi-factor authentication-registratie beheren door een beleid waarmee u kunt configureren:</span><span class="sxs-lookup"><span data-stu-id="e106f-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="e106f-345">Set Hallo gebruikers en groepen Hallo beleid van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="e106f-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="e106f-346">![MFA-beleid](./media/active-directory-identityprotection/1020.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="e106f-347">Set Hallo besturingselementen toobe afgedwongen wanneer Hallo beleid activeert::</span><span class="sxs-lookup"><span data-stu-id="e106f-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="e106f-348">![MFA-beleid](./media/active-directory-identityprotection/1021.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="e106f-349">Hallo-status van uw beleid switch:</span><span class="sxs-lookup"><span data-stu-id="e106f-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="e106f-350">![MFA-beleid](./media/active-directory-identityprotection/403.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="e106f-351">Status van huidige registratie Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="e106f-351">View hello current registration status:</span></span>

    <span data-ttu-id="e106f-352">![MFA-beleid](./media/active-directory-identityprotection/1022.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="e106f-353">Voor een overzicht van Hallo gerelateerde gebruikerservaring, Zie:</span><span class="sxs-lookup"><span data-stu-id="e106f-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="e106f-354">[Registratie voor meervoudige authenticatiestroom](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="e106f-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="e106f-355">[Aanmelden-ervaringen met Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="e106f-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="e106f-356">**dialoogvenster tooopen Hallo-gerelateerde configuratie**:</span><span class="sxs-lookup"><span data-stu-id="e106f-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="e106f-357">Op Hallo **Azure AD Identity Protection** blade in Hallo **configureren** sectie, klikt u op **multi-factor authentication-registratie**.</span><span class="sxs-lookup"><span data-stu-id="e106f-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="e106f-358">![MFA-beleid](./media/active-directory-identityprotection/1019.png "MFA-beleid")</span><span class="sxs-lookup"><span data-stu-id="e106f-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="e106f-359">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e106f-359">Next steps</span></span>
* [<span data-ttu-id="e106f-360">Channel 9: Azure AD en Identity weergeven: Identity Protection Preview</span><span class="sxs-lookup"><span data-stu-id="e106f-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="e106f-361">Inschakelen van beveiliging voor Azure Active Directory-identiteit</span><span class="sxs-lookup"><span data-stu-id="e106f-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="e106f-362">Beveiligingsproblemen die worden gedetecteerd door Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e106f-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="e106f-363">Azure Active Directory-risicogebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="e106f-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="e106f-364">Azure Active Directory: Identity Protection-meldingen</span><span class="sxs-lookup"><span data-stu-id="e106f-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="e106f-365">Playbook voor Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e106f-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="e106f-366">Azure Active Directory: Identity Protection verklarende woordenlijst</span><span class="sxs-lookup"><span data-stu-id="e106f-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="e106f-367">Aanmelden-ervaring met Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e106f-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="e106f-368">Azure Active Directory: Identity Protection - hoe toounblock gebruikers</span><span class="sxs-lookup"><span data-stu-id="e106f-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="e106f-369">Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e106f-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
