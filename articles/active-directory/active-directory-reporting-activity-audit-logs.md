---
title: aaaAudit activiteit rapporten in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Inleiding toohello audit activiteitsrapporten in hello Azure Active Directory-portal
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="e491c-103">Activiteitsrapporten in Azure Active Directory-beheerportal Hallo controleren</span><span class="sxs-lookup"><span data-stu-id="e491c-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="e491c-104">Met rapportage in Azure Active Directory (Azure AD), kunt u de gewenste toodetermine hoe uw omgeving doet Hallo-informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="e491c-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="e491c-105">architectuur van rapportage in Azure AD Hallo bestaat uit Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="e491c-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="e491c-106">**Activiteit**</span><span class="sxs-lookup"><span data-stu-id="e491c-106">**Activity**</span></span> 
    - <span data-ttu-id="e491c-107">**Aanmelden activiteiten** – informatie over het gebruik van Hallo van beheerde toepassingen en gebruikersactiviteiten aanmelden</span><span class="sxs-lookup"><span data-stu-id="e491c-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="e491c-108">**Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="e491c-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="e491c-109">**Beveiliging**</span><span class="sxs-lookup"><span data-stu-id="e491c-109">**Security**</span></span> 
    - <span data-ttu-id="e491c-110">**Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="e491c-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="e491c-111">Zie Riskante aanmeldingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e491c-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="e491c-112">**Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="e491c-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="e491c-113">Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e491c-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="e491c-114">In dit onderwerp biedt een overzicht van Hallo audit activiteiten.</span><span class="sxs-lookup"><span data-stu-id="e491c-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="e491c-115">Wie toegang heeft tot Hallo gegevens?</span><span class="sxs-lookup"><span data-stu-id="e491c-115">Who can access hello data?</span></span>
* <span data-ttu-id="e491c-116">Gebruikers met de rol beheerder beveiliging of beveiliging Reader Hallo</span><span class="sxs-lookup"><span data-stu-id="e491c-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="e491c-117">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="e491c-117">Global Admins</span></span>
* <span data-ttu-id="e491c-118">Afzonderlijke gebruikers (niet-beheerders) kunnen hun eigen activiteiten zien</span><span class="sxs-lookup"><span data-stu-id="e491c-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="e491c-119">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="e491c-119">Audit logs</span></span>

<span data-ttu-id="e491c-120">Hallo controlelogboeken in Azure Active Directory bieden records van het systeemactiviteiten voor naleving.</span><span class="sxs-lookup"><span data-stu-id="e491c-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="e491c-121">Uw eerste vermelding punt tooall controle van gegevens is **controlelogboeken** in Hallo **activiteit** sectie van **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e491c-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="e491c-122">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/61.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="e491c-123">Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:</span><span class="sxs-lookup"><span data-stu-id="e491c-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="e491c-124">Hallo-datum en tijd van Hallo-instantie</span><span class="sxs-lookup"><span data-stu-id="e491c-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="e491c-125">Hallo initiator / actor (*die*) van een activiteit</span><span class="sxs-lookup"><span data-stu-id="e491c-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="e491c-126">Hallo activiteit (*wat*)</span><span class="sxs-lookup"><span data-stu-id="e491c-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="e491c-127">Hallo-doel</span><span class="sxs-lookup"><span data-stu-id="e491c-127">hello target</span></span>

<span data-ttu-id="e491c-128">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/18.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="e491c-129">U kunt de lijstweergave Hallo aanpassen door te klikken op **kolommen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="e491c-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="e491c-130">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/19.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="e491c-131">Dit kunt u aanvullende velden toodisplay of verwijderen van de velden die al worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e491c-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="e491c-132">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/21.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="e491c-133">Door te klikken op een item in de lijstweergave hello, moet u alle beschikbare details over het ophalen.</span><span class="sxs-lookup"><span data-stu-id="e491c-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="e491c-134">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/22.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="e491c-135">Controlelogboeken filteren</span><span class="sxs-lookup"><span data-stu-id="e491c-135">Filtering audit logs</span></span>

<span data-ttu-id="e491c-136">toonarrow omlaag Hallo tooa gegevensniveau dat geldt voor u, kunt u Hallo audit gegevens filteren met behulp van de volgende velden Hallo gerapporteerd:</span><span class="sxs-lookup"><span data-stu-id="e491c-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="e491c-137">Datumbereik</span><span class="sxs-lookup"><span data-stu-id="e491c-137">Date range</span></span>
- <span data-ttu-id="e491c-138">Gestart door (actor)</span><span class="sxs-lookup"><span data-stu-id="e491c-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="e491c-139">Category</span><span class="sxs-lookup"><span data-stu-id="e491c-139">Category</span></span>
- <span data-ttu-id="e491c-140">Resourcetype van activiteit</span><span class="sxs-lookup"><span data-stu-id="e491c-140">Activity resource type</span></span>
- <span data-ttu-id="e491c-141">Activiteit</span><span class="sxs-lookup"><span data-stu-id="e491c-141">Activity</span></span>

<span data-ttu-id="e491c-142">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/23.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="e491c-143">Hallo **datumbereik** filter schakelt tooyou toodefine een tijdsspanne voor Hallo gegevens geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e491c-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="e491c-144">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="e491c-144">Possible values are:</span></span>

- <span data-ttu-id="e491c-145">1 maand</span><span class="sxs-lookup"><span data-stu-id="e491c-145">1 month</span></span>
- <span data-ttu-id="e491c-146">7 dagen</span><span class="sxs-lookup"><span data-stu-id="e491c-146">7 days</span></span>
- <span data-ttu-id="e491c-147">24 uur</span><span class="sxs-lookup"><span data-stu-id="e491c-147">24 hours</span></span>
- <span data-ttu-id="e491c-148">Aangepast telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="e491c-148">Custom</span></span>

<span data-ttu-id="e491c-149">Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.</span><span class="sxs-lookup"><span data-stu-id="e491c-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="e491c-150">Hallo **gestart door** filter kunt u toodefine een actor-naam of de UPN (User Principal Name).</span><span class="sxs-lookup"><span data-stu-id="e491c-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="e491c-151">Hallo **categorie** filter kunt u tooselect Hallo filter te volgen:</span><span class="sxs-lookup"><span data-stu-id="e491c-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="e491c-152">Alle</span><span class="sxs-lookup"><span data-stu-id="e491c-152">All</span></span>
- <span data-ttu-id="e491c-153">Hoofdcategorie</span><span class="sxs-lookup"><span data-stu-id="e491c-153">Core category</span></span>
- <span data-ttu-id="e491c-154">Hoofddirectory</span><span class="sxs-lookup"><span data-stu-id="e491c-154">Core directory</span></span>
- <span data-ttu-id="e491c-155">Wachtwoordbeheer via selfservice</span><span class="sxs-lookup"><span data-stu-id="e491c-155">Self-service password management</span></span>
- <span data-ttu-id="e491c-156">Groepsbeheer via selfservice</span><span class="sxs-lookup"><span data-stu-id="e491c-156">Self-service group management</span></span>
- <span data-ttu-id="e491c-157">Account inrichten - Automatische wachtwoordoverschakeling</span><span class="sxs-lookup"><span data-stu-id="e491c-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="e491c-158">Uitgenodigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="e491c-158">Invited users</span></span>
- <span data-ttu-id="e491c-159">MIM-service</span><span class="sxs-lookup"><span data-stu-id="e491c-159">MIM service</span></span>
- <span data-ttu-id="e491c-160">Identiteitsbeveiliging</span><span class="sxs-lookup"><span data-stu-id="e491c-160">Identity Protection</span></span>
- <span data-ttu-id="e491c-161">B2C</span><span class="sxs-lookup"><span data-stu-id="e491c-161">B2C</span></span>

<span data-ttu-id="e491c-162">Hallo **activiteit brontype** filter kunt u een van de volgende Hallo filtert tooselect:</span><span class="sxs-lookup"><span data-stu-id="e491c-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="e491c-163">Alle</span><span class="sxs-lookup"><span data-stu-id="e491c-163">All</span></span> 
- <span data-ttu-id="e491c-164">Groep</span><span class="sxs-lookup"><span data-stu-id="e491c-164">Group</span></span>
- <span data-ttu-id="e491c-165">Directory</span><span class="sxs-lookup"><span data-stu-id="e491c-165">Directory</span></span>
- <span data-ttu-id="e491c-166">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="e491c-166">User</span></span>
- <span data-ttu-id="e491c-167">Toepassing</span><span class="sxs-lookup"><span data-stu-id="e491c-167">Application</span></span>
- <span data-ttu-id="e491c-168">Beleid</span><span class="sxs-lookup"><span data-stu-id="e491c-168">Policy</span></span>
- <span data-ttu-id="e491c-169">Apparaat</span><span class="sxs-lookup"><span data-stu-id="e491c-169">Device</span></span>
- <span data-ttu-id="e491c-170">Overige</span><span class="sxs-lookup"><span data-stu-id="e491c-170">Other</span></span>

<span data-ttu-id="e491c-171">Wanneer u selecteert **groep** als **activiteit brontype**, dat u een extra filtercategorie waarmee u tooalso bieden een **bron**:</span><span class="sxs-lookup"><span data-stu-id="e491c-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="e491c-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="e491c-172">Azure AD</span></span>
- <span data-ttu-id="e491c-173">O365</span><span class="sxs-lookup"><span data-stu-id="e491c-173">O365</span></span>


<span data-ttu-id="e491c-174">Hallo **activiteit** filter is gebaseerd op het Hallo-categorie en activiteit resource type selectie die u maakt.</span><span class="sxs-lookup"><span data-stu-id="e491c-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="e491c-175">U kunt een bepaalde activiteit of wilt u toosee Kies alle selecteren.</span><span class="sxs-lookup"><span data-stu-id="e491c-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="e491c-176">U kunt Hallo lijst van alle activiteiten van de Audit ophalen met behulp van Hallo Graph API https://graph.windows.net/$ activiteiten-tenantdomain/auditActivityTypes? api-versie = Bèta, waarbij $tenantdomain = uw domeinnaam of Raadpleeg toohello artikel [rapport van de audit gebeurtenissen](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="e491c-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="e491c-177">Snelkoppelingen naar controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="e491c-177">Audit logs shortcuts</span></span>

<span data-ttu-id="e491c-178">Bovendien te**Azure Active Directory**, hello Azure-portal biedt u twee extra toegangspunten tooaudit gegevens:</span><span class="sxs-lookup"><span data-stu-id="e491c-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="e491c-179">Gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="e491c-179">Users and groups</span></span>
- <span data-ttu-id="e491c-180">Bedrijfstoepassingen</span><span class="sxs-lookup"><span data-stu-id="e491c-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="e491c-181">Controlelogboeken voor gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="e491c-181">Users and groups audit logs</span></span>

<span data-ttu-id="e491c-182">Met gebruikers en groepen gebaseerde controlerapporten, kun je antwoorden tooquestions zoals:</span><span class="sxs-lookup"><span data-stu-id="e491c-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="e491c-183">Welke typen updates zijn toegepast Hallo gebruikers?</span><span class="sxs-lookup"><span data-stu-id="e491c-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="e491c-184">Hoeveel gebruikers zijn gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="e491c-184">How many users were changed?</span></span>

- <span data-ttu-id="e491c-185">Hoeveel wachtwoorden zijn gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="e491c-185">How many passwords were changed?</span></span>

- <span data-ttu-id="e491c-186">Wat heeft een beheerder in een directory gedaan?</span><span class="sxs-lookup"><span data-stu-id="e491c-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="e491c-187">Wat zijn Hallo-groepen die zijn toegevoegd?</span><span class="sxs-lookup"><span data-stu-id="e491c-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="e491c-188">Zijn er groepen met wijzigingen in het lidmaatschap?</span><span class="sxs-lookup"><span data-stu-id="e491c-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="e491c-189">Hallo-eigenaars van groep zijn gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="e491c-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="e491c-190">Welke licenties zijn toegewezen tooa groep of een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="e491c-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="e491c-191">Als u wilt dat alleen tooreview controle van de gegevens die zijn gerelateerd toousers en groepen, vindt u een gefilterde weergave onder **controlelogboeken** in Hallo **activiteit** sectie Hallo **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="e491c-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="e491c-192">Dit beginpunt heeft **Gebruikers en groepen** als vooraf geselecteerd **Type activiteitsresource**.</span><span class="sxs-lookup"><span data-stu-id="e491c-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="e491c-193">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/93.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="e491c-194">Controlelogboeken voor bedrijfstoepassingen</span><span class="sxs-lookup"><span data-stu-id="e491c-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="e491c-195">Controleren op basis van een toepassing met de rapporten, kunt u antwoorden tooquestions zoals krijgen:</span><span class="sxs-lookup"><span data-stu-id="e491c-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="e491c-196">Wat zijn Hallo-toepassingen die zijn toegevoegd of bijgewerkt?</span><span class="sxs-lookup"><span data-stu-id="e491c-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="e491c-197">Wat zijn Hallo-toepassingen die zijn verwijderd?</span><span class="sxs-lookup"><span data-stu-id="e491c-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="e491c-198">Is de service-principal van een toepassing gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="e491c-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="e491c-199">Hallo-namen van toepassingen zijn gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="e491c-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="e491c-200">Wie heeft toestemming tooan toepassing?</span><span class="sxs-lookup"><span data-stu-id="e491c-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="e491c-201">Als u wilt dat alleen tooreview controle van de gegevens die zijn gerelateerd tooyour toepassingen, kunt u vinden in een gefilterde weergave onder **controlelogboeken** in Hallo **activiteit** sectie Hallo **bedrijfstoepassingen**  blade.</span><span class="sxs-lookup"><span data-stu-id="e491c-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="e491c-202">Dit beginpunt heeft **Bedrijfstoepassingen** als vooraf geselecteerd **Type activiteitsresource**.</span><span class="sxs-lookup"><span data-stu-id="e491c-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="e491c-203">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/134.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="e491c-204">U kunt deze weergave verder omlaag toojust filteren **groepen** of alleen **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="e491c-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="e491c-205">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/25.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="e491c-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="e491c-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e491c-206">Next steps</span></span>

<span data-ttu-id="e491c-207">Zie voor een overzicht van reporting Hallo [rapportage van Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e491c-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

