---
title: Controleactiviteitenrapporten in Azure Active Directory Portal | Microsoft Docs
description: Ontdek de controleactiviteitenrapporten in de Azure Active Directory Portal
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
ms.openlocfilehash: f2d0332d815c82d7d47625e020de2e9c5099deeb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="9cb92-103">Controleactiviteitenrapporten in Azure Active Directory Portal</span><span class="sxs-lookup"><span data-stu-id="9cb92-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="9cb92-104">Met rapporten in Azure Active Directory ontvangt u alle informatie die nodig is om te bepalen hoe het gaat met uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="9cb92-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="9cb92-105">De rapportstructuur in Azure AD bestaat uit de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="9cb92-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="9cb92-106">**Activiteit**</span><span class="sxs-lookup"><span data-stu-id="9cb92-106">**Activity**</span></span> 
    - <span data-ttu-id="9cb92-107">**Aanmeldactiviteiten**: informatie over het gebruik van beheerde toepassingen en aanmeldactiviteiten van gebruikers</span><span class="sxs-lookup"><span data-stu-id="9cb92-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="9cb92-108">**Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="9cb92-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="9cb92-109">**Beveiliging**</span><span class="sxs-lookup"><span data-stu-id="9cb92-109">**Security**</span></span> 
    - <span data-ttu-id="9cb92-110">**Riskante aanmeldingen** - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is.</span><span class="sxs-lookup"><span data-stu-id="9cb92-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="9cb92-111">Zie Riskante aanmeldingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9cb92-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="9cb92-112">**Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="9cb92-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="9cb92-113">Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9cb92-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="9cb92-114">In dit onderwerp vindt u meer informatie over de controleactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="9cb92-114">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="9cb92-115">Wie heeft er toegang tot de gegevens?</span><span class="sxs-lookup"><span data-stu-id="9cb92-115">Who can access the data?</span></span>
* <span data-ttu-id="9cb92-116">Gebruikers met de rol Beveiligingsbeheerder of Beveiligingslezer</span><span class="sxs-lookup"><span data-stu-id="9cb92-116">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="9cb92-117">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="9cb92-117">Global Admins</span></span>
* <span data-ttu-id="9cb92-118">Afzonderlijke gebruikers (niet-beheerders) kunnen hun eigen activiteiten zien</span><span class="sxs-lookup"><span data-stu-id="9cb92-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="9cb92-119">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="9cb92-119">Audit logs</span></span>

<span data-ttu-id="9cb92-120">In de controlelogboeken in Azure Active Directory staan records van systeemactiviteiten voor naleving.</span><span class="sxs-lookup"><span data-stu-id="9cb92-120">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="9cb92-121">Uw eerste beginpunt voor alle controlegegevens is **Controlelogboeken** in het gedeelte **Activiteit** van **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9cb92-121">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="9cb92-122">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/61.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="9cb92-123">Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:</span><span class="sxs-lookup"><span data-stu-id="9cb92-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="9cb92-124">de datum en tijd van de gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="9cb92-124">the date and time of the occurrence</span></span>
- <span data-ttu-id="9cb92-125">de initiator/actor (*wie*) van een activiteit</span><span class="sxs-lookup"><span data-stu-id="9cb92-125">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="9cb92-126">de activiteit (*wat*)</span><span class="sxs-lookup"><span data-stu-id="9cb92-126">the activity (*what*)</span></span> 
- <span data-ttu-id="9cb92-127">het doel</span><span class="sxs-lookup"><span data-stu-id="9cb92-127">the target</span></span>

<span data-ttu-id="9cb92-128">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/18.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="9cb92-129">U kunt de lijstweergave aanpassen door te klikken op **Kolommen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="9cb92-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="9cb92-130">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/19.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="9cb92-131">Hiermee kunt u extra velden weergeven of velden verwijderen die al worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9cb92-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="9cb92-132">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/21.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="9cb92-133">Wanneer u op een item in de lijstweergave klikt, krijgt u er alle beschikbare informatie over te zien.</span><span class="sxs-lookup"><span data-stu-id="9cb92-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="9cb92-134">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/22.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="9cb92-135">Controlelogboeken filteren</span><span class="sxs-lookup"><span data-stu-id="9cb92-135">Filtering audit logs</span></span>

<span data-ttu-id="9cb92-136">Als u de gerapporteerde gegevens wilt beperken tot een niveau dat geschikt is voor u, kunt u de controlegegevens filteren met de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="9cb92-136">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="9cb92-137">Datumbereik</span><span class="sxs-lookup"><span data-stu-id="9cb92-137">Date range</span></span>
- <span data-ttu-id="9cb92-138">Gestart door (actor)</span><span class="sxs-lookup"><span data-stu-id="9cb92-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="9cb92-139">Category</span><span class="sxs-lookup"><span data-stu-id="9cb92-139">Category</span></span>
- <span data-ttu-id="9cb92-140">Resourcetype van activiteit</span><span class="sxs-lookup"><span data-stu-id="9cb92-140">Activity resource type</span></span>
- <span data-ttu-id="9cb92-141">Activiteit</span><span class="sxs-lookup"><span data-stu-id="9cb92-141">Activity</span></span>

<span data-ttu-id="9cb92-142">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/23.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="9cb92-143">Met het filter **datumbereik** kunt u een tijdsbestek opgeven voor de geretourneerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="9cb92-143">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="9cb92-144">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="9cb92-144">Possible values are:</span></span>

- <span data-ttu-id="9cb92-145">1 maand</span><span class="sxs-lookup"><span data-stu-id="9cb92-145">1 month</span></span>
- <span data-ttu-id="9cb92-146">7 dagen</span><span class="sxs-lookup"><span data-stu-id="9cb92-146">7 days</span></span>
- <span data-ttu-id="9cb92-147">24 uur</span><span class="sxs-lookup"><span data-stu-id="9cb92-147">24 hours</span></span>
- <span data-ttu-id="9cb92-148">Aangepast telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="9cb92-148">Custom</span></span>

<span data-ttu-id="9cb92-149">Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.</span><span class="sxs-lookup"><span data-stu-id="9cb92-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="9cb92-150">Met het filter **gestart door** kunt u de naam of UPN (Universal Principal Name) van een actor definiëren.</span><span class="sxs-lookup"><span data-stu-id="9cb92-150">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="9cb92-151">Met het filter **aanmeldingsstatus** kunt u een van de volgende filters selecteren:</span><span class="sxs-lookup"><span data-stu-id="9cb92-151">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="9cb92-152">Alle</span><span class="sxs-lookup"><span data-stu-id="9cb92-152">All</span></span>
- <span data-ttu-id="9cb92-153">Hoofdcategorie</span><span class="sxs-lookup"><span data-stu-id="9cb92-153">Core category</span></span>
- <span data-ttu-id="9cb92-154">Hoofddirectory</span><span class="sxs-lookup"><span data-stu-id="9cb92-154">Core directory</span></span>
- <span data-ttu-id="9cb92-155">Wachtwoordbeheer via selfservice</span><span class="sxs-lookup"><span data-stu-id="9cb92-155">Self-service password management</span></span>
- <span data-ttu-id="9cb92-156">Groepsbeheer via selfservice</span><span class="sxs-lookup"><span data-stu-id="9cb92-156">Self-service group management</span></span>
- <span data-ttu-id="9cb92-157">Account inrichten - Automatische wachtwoordoverschakeling</span><span class="sxs-lookup"><span data-stu-id="9cb92-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="9cb92-158">Uitgenodigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="9cb92-158">Invited users</span></span>
- <span data-ttu-id="9cb92-159">MIM-service</span><span class="sxs-lookup"><span data-stu-id="9cb92-159">MIM service</span></span>
- <span data-ttu-id="9cb92-160">Identiteitsbeveiliging</span><span class="sxs-lookup"><span data-stu-id="9cb92-160">Identity Protection</span></span>
- <span data-ttu-id="9cb92-161">B2C</span><span class="sxs-lookup"><span data-stu-id="9cb92-161">B2C</span></span>

<span data-ttu-id="9cb92-162">Met het filter **type activiteitsresource** kunt u een van de volgende filters selecteren:</span><span class="sxs-lookup"><span data-stu-id="9cb92-162">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="9cb92-163">Alle</span><span class="sxs-lookup"><span data-stu-id="9cb92-163">All</span></span> 
- <span data-ttu-id="9cb92-164">Groep</span><span class="sxs-lookup"><span data-stu-id="9cb92-164">Group</span></span>
- <span data-ttu-id="9cb92-165">Directory</span><span class="sxs-lookup"><span data-stu-id="9cb92-165">Directory</span></span>
- <span data-ttu-id="9cb92-166">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="9cb92-166">User</span></span>
- <span data-ttu-id="9cb92-167">Toepassing</span><span class="sxs-lookup"><span data-stu-id="9cb92-167">Application</span></span>
- <span data-ttu-id="9cb92-168">Beleid</span><span class="sxs-lookup"><span data-stu-id="9cb92-168">Policy</span></span>
- <span data-ttu-id="9cb92-169">Apparaat</span><span class="sxs-lookup"><span data-stu-id="9cb92-169">Device</span></span>
- <span data-ttu-id="9cb92-170">Overige</span><span class="sxs-lookup"><span data-stu-id="9cb92-170">Other</span></span>

<span data-ttu-id="9cb92-171">Wanneer u **Groep** selecteert als **type activiteitsresource**, krijgt u een extra filtercategorie waarmee u ook een **Bron** kunt opgeven:</span><span class="sxs-lookup"><span data-stu-id="9cb92-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="9cb92-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cb92-172">Azure AD</span></span>
- <span data-ttu-id="9cb92-173">O365</span><span class="sxs-lookup"><span data-stu-id="9cb92-173">O365</span></span>


<span data-ttu-id="9cb92-174">Het filter **activiteit** is gebaseerd op de selectie die u maakt voor de categorie en het type activiteitsresource.</span><span class="sxs-lookup"><span data-stu-id="9cb92-174">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="9cb92-175">U kunt een specifieke activiteit of alle activiteiten selecteren.</span><span class="sxs-lookup"><span data-stu-id="9cb92-175">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="9cb92-176">U kunt de lijst met alle controle-activiteiten opvragen met behulp van de Graph API https://graph.windows.net/$tenantdomein/activities/auditActivityTypes?api-version=beta, waarbij u $tenantdomain vervangt door de naam van uw domein, of raadpleeg het artikel [Azure Active Directory audit report events](active-directory-reporting-audit-events.md) (Gebeurtenissen in Azure Active Directory-controlerapporten).</span><span class="sxs-lookup"><span data-stu-id="9cb92-176">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="9cb92-177">Snelkoppelingen naar controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="9cb92-177">Audit logs shortcuts</span></span>

<span data-ttu-id="9cb92-178">Naast **Azure Active Directory** biedt de Azure Portal twee extra beginpunten voor gegevenscontrole:</span><span class="sxs-lookup"><span data-stu-id="9cb92-178">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="9cb92-179">Gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="9cb92-179">Users and groups</span></span>
- <span data-ttu-id="9cb92-180">Bedrijfstoepassingen</span><span class="sxs-lookup"><span data-stu-id="9cb92-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="9cb92-181">Controlelogboeken voor gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="9cb92-181">Users and groups audit logs</span></span>

<span data-ttu-id="9cb92-182">Met de controlerapporten op basis van gebruikers en groepen krijgt u antwoord op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="9cb92-182">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="9cb92-183">Welke soorten updates zijn toegepast op de gebruikers?</span><span class="sxs-lookup"><span data-stu-id="9cb92-183">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="9cb92-184">Hoeveel gebruikers zijn gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-184">How many users were changed?</span></span>

- <span data-ttu-id="9cb92-185">Hoeveel wachtwoorden zijn gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-185">How many passwords were changed?</span></span>

- <span data-ttu-id="9cb92-186">Wat heeft een beheerder in een directory gedaan?</span><span class="sxs-lookup"><span data-stu-id="9cb92-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="9cb92-187">Welke groepen zijn toegevoegd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-187">What are the groups that have been added?</span></span>

- <span data-ttu-id="9cb92-188">Zijn er groepen met wijzigingen in het lidmaatschap?</span><span class="sxs-lookup"><span data-stu-id="9cb92-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="9cb92-189">Zijn de eigenaren van een groep gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-189">Have the owners of group been changed?</span></span>

- <span data-ttu-id="9cb92-190">Welke licenties zijn toegewezen aan een groep of een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="9cb92-190">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="9cb92-191">Als u alleen controlegegevens wilt bekijken die aan gebruikers en groepen zijn gerelateerd, kunt u een gefilterde weergave openen via **Controlelogboeken** in het gedeelte **Activiteit** van **Gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="9cb92-191">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="9cb92-192">Dit beginpunt heeft **Gebruikers en groepen** als vooraf geselecteerd **Type activiteitsresource**.</span><span class="sxs-lookup"><span data-stu-id="9cb92-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="9cb92-193">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/93.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="9cb92-194">Controlelogboeken voor bedrijfstoepassingen</span><span class="sxs-lookup"><span data-stu-id="9cb92-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="9cb92-195">Met de controlerapporten op basis van toepassingen krijgt u antwoord op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="9cb92-195">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="9cb92-196">Welke toepassingen zijn toegevoegd of bijgewerkt?</span><span class="sxs-lookup"><span data-stu-id="9cb92-196">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="9cb92-197">Welke toepassingen zijn verwijderd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-197">What are the applications that have been removed?</span></span>
* <span data-ttu-id="9cb92-198">Is de service-principal van een toepassing gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="9cb92-199">Zijn de namen van toepassingen gewijzigd?</span><span class="sxs-lookup"><span data-stu-id="9cb92-199">Have the names of applications been changed?</span></span>
* <span data-ttu-id="9cb92-200">Wie heeft toestemming gegeven voor een toepassing?</span><span class="sxs-lookup"><span data-stu-id="9cb92-200">Who gave consent to an application?</span></span>

<span data-ttu-id="9cb92-201">Als u alleen controlegegevens wilt bekijken die aan uw toepassingen zijn gerelateerd, kunt u een gefilterde weergave openen via **Controlelogboeken** in het gedeelte **Activiteit** van de blade **Bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="9cb92-201">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="9cb92-202">Dit beginpunt heeft **Bedrijfstoepassingen** als vooraf geselecteerd **Type activiteitsresource**.</span><span class="sxs-lookup"><span data-stu-id="9cb92-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="9cb92-203">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/134.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="9cb92-204">U kunt deze weergave verder filteren naar alleen **Groepen** of alleen **Gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="9cb92-204">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="9cb92-205">![Controlelogboeken](./media/active-directory-reporting-activity-audit-logs/25.png "Controlelogboeken")</span><span class="sxs-lookup"><span data-stu-id="9cb92-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="9cb92-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9cb92-206">Next steps</span></span>

<span data-ttu-id="9cb92-207">Zie [Azure Active Directory-rapportage](active-directory-reporting-azure-portal.md) voor een overzicht van de rapportage.</span><span class="sxs-lookup"><span data-stu-id="9cb92-207">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

