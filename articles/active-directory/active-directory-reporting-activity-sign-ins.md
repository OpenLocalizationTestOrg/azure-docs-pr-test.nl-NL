---
title: Aanmeldactiviteitenrapporten in Azure Active Directory Portal | Microsoft Docs
description: Ontdek de aanmeldactiviteitenrapporten in de Azure Active Directory Portal
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="afb0b-103">Aanmeldactiviteitenrapporten in Azure Active Directory Portal</span><span class="sxs-lookup"><span data-stu-id="afb0b-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="afb0b-104">Met Azure AD-rapporten (Azure Active Directory) in [Azure Portal](https://portal.azure.com) ontvangt u alle informatie die nodig is om te bepalen hoe het gaat met uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="afb0b-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="afb0b-105">De rapportstructuur in Azure Active Directory bestaat uit de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="afb0b-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="afb0b-106">**Activiteit**</span><span class="sxs-lookup"><span data-stu-id="afb0b-106">**Activity**</span></span> 
    - <span data-ttu-id="afb0b-107">**Aanmeldactiviteiten**: informatie over het gebruik van beheerde toepassingen en aanmeldactiviteiten van gebruikers</span><span class="sxs-lookup"><span data-stu-id="afb0b-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="afb0b-108">**Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="afb0b-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="afb0b-109">**Beveiliging**</span><span class="sxs-lookup"><span data-stu-id="afb0b-109">**Security**</span></span> 
    - <span data-ttu-id="afb0b-110">**Riskante aanmeldingen** - Een riskante aanmelding is een indicator van een aanmeldingspoging die mogelijk is uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is.</span><span class="sxs-lookup"><span data-stu-id="afb0b-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="afb0b-111">Zie Riskante aanmeldingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="afb0b-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="afb0b-112">**Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="afb0b-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="afb0b-113">Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="afb0b-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="afb0b-114">In dit onderwerp vindt u meer informatie over de aanmeldactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="afb0b-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="afb0b-115">Vereiste</span><span class="sxs-lookup"><span data-stu-id="afb0b-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="afb0b-116">Wie heeft er toegang tot de gegevens?</span><span class="sxs-lookup"><span data-stu-id="afb0b-116">Who can access the data?</span></span>
* <span data-ttu-id="afb0b-117">Gebruikers met de rol Beveiligingsbeheerder of Beveiligingslezer</span><span class="sxs-lookup"><span data-stu-id="afb0b-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="afb0b-118">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="afb0b-118">Global Admins</span></span>
* <span data-ttu-id="afb0b-119">Alle gebruiker (niet-beheerders) hebben toegang tot hun eigen aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="afb0b-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="afb0b-120">Welke Azure AD-licentie heb ik nodig voor toegang tot aanmeldingsactiviteiten?</span><span class="sxs-lookup"><span data-stu-id="afb0b-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="afb0b-121">Uw tenant moet beschikken over een Azure AD Premium-licentie om het rapport met alle aanmeldingsactiviteiten te kunnen raadplegen</span><span class="sxs-lookup"><span data-stu-id="afb0b-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="afb0b-122">Aanmeldactiviteiten</span><span class="sxs-lookup"><span data-stu-id="afb0b-122">Signs-in activities</span></span>

<span data-ttu-id="afb0b-123">In de informatie die wordt aangeboden in het rapport over aanmeldactiviteiten van gebruikers, vindt u antwoord op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="afb0b-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="afb0b-124">Wat is het aanmeldingspatroon van een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="afb0b-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="afb0b-125">Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?</span><span class="sxs-lookup"><span data-stu-id="afb0b-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="afb0b-126">Wat is de status van deze aanmeldingen?</span><span class="sxs-lookup"><span data-stu-id="afb0b-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="afb0b-127">Uw eerste ingangspunt voor alle aanmeldingsactiviteitgegevens is **Aanmeldingen** in het gedeelte activiteit van **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="afb0b-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="afb0b-128">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/61.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="afb0b-129">Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:</span><span class="sxs-lookup"><span data-stu-id="afb0b-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="afb0b-130">de gerelateerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="afb0b-130">the related user</span></span>
- <span data-ttu-id="afb0b-131">de toepassing waarbij de gebruiker is aangemeld</span><span class="sxs-lookup"><span data-stu-id="afb0b-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="afb0b-132">de aanmeldingsstatus</span><span class="sxs-lookup"><span data-stu-id="afb0b-132">the sign-in status</span></span>
- <span data-ttu-id="afb0b-133">de aanmeldingstijd</span><span class="sxs-lookup"><span data-stu-id="afb0b-133">the sign-in time</span></span>

<span data-ttu-id="afb0b-134">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/41.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-135">U kunt de lijstweergave aanpassen door te klikken op **Kolommen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="afb0b-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="afb0b-136">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/19.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-137">Hiermee kunt u extra velden weergeven of velden verwijderen die al worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="afb0b-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="afb0b-138">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/42.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-139">Wanneer u op een item in de lijstweergave klikt, krijgt u er alle beschikbare informatie over te zien.</span><span class="sxs-lookup"><span data-stu-id="afb0b-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="afb0b-140">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/43.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="afb0b-141">Aanmeldingsactiviteiten filteren</span><span class="sxs-lookup"><span data-stu-id="afb0b-141">Filtering sign-in activities</span></span>

<span data-ttu-id="afb0b-142">Als u de gerapporteerde gegevens wilt beperken tot een bepaald niveau, kunt u de aanmeldingsgegevens filteren met de volgende velden:</span><span class="sxs-lookup"><span data-stu-id="afb0b-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="afb0b-143">Tijdsinterval</span><span class="sxs-lookup"><span data-stu-id="afb0b-143">Time interval</span></span>
- <span data-ttu-id="afb0b-144">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="afb0b-144">User</span></span>
- <span data-ttu-id="afb0b-145">Toepassing</span><span class="sxs-lookup"><span data-stu-id="afb0b-145">Application</span></span>
- <span data-ttu-id="afb0b-146">Client</span><span class="sxs-lookup"><span data-stu-id="afb0b-146">Client</span></span>
- <span data-ttu-id="afb0b-147">Aanmeldingsstatus</span><span class="sxs-lookup"><span data-stu-id="afb0b-147">Sign-in status</span></span>

<span data-ttu-id="afb0b-148">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/44.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="afb0b-149">Met het filter **tijdsinterval** kunt u een tijdsbestek opgeven voor de geretourneerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="afb0b-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="afb0b-150">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="afb0b-150">Possible values are:</span></span>

- <span data-ttu-id="afb0b-151">1 maand</span><span class="sxs-lookup"><span data-stu-id="afb0b-151">1 month</span></span>
- <span data-ttu-id="afb0b-152">7 dagen</span><span class="sxs-lookup"><span data-stu-id="afb0b-152">7 days</span></span>
- <span data-ttu-id="afb0b-153">24 uur</span><span class="sxs-lookup"><span data-stu-id="afb0b-153">24 hours</span></span>
- <span data-ttu-id="afb0b-154">Aangepast telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="afb0b-154">Custom</span></span>

<span data-ttu-id="afb0b-155">Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.</span><span class="sxs-lookup"><span data-stu-id="afb0b-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="afb0b-156">Met het filter **gebruiker** kunt u de naam of de UPN (User Principal Name) van de gewenste gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="afb0b-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="afb0b-157">Met het filter **toepassing** kunt u de naam van de gewenste toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="afb0b-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="afb0b-158">Met het filter **client** kunt u informatie over het gewenste apparaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="afb0b-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="afb0b-159">Met het filter **aanmeldingsstatus** kunt u een van de volgende filters selecteren:</span><span class="sxs-lookup"><span data-stu-id="afb0b-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="afb0b-160">Alle</span><span class="sxs-lookup"><span data-stu-id="afb0b-160">All</span></span>
- <span data-ttu-id="afb0b-161">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="afb0b-161">Success</span></span>
- <span data-ttu-id="afb0b-162">Fout</span><span class="sxs-lookup"><span data-stu-id="afb0b-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="afb0b-163">Snelkoppelingen voor aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="afb0b-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="afb0b-164">Naast Azure Active Directory biedt de Azure Portal twee extra toegangspunten voor aanmeldingsactiviteitgegevens:</span><span class="sxs-lookup"><span data-stu-id="afb0b-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="afb0b-165">Gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="afb0b-165">Users and groups</span></span>
- <span data-ttu-id="afb0b-166">Bedrijfstoepassingen</span><span class="sxs-lookup"><span data-stu-id="afb0b-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="afb0b-167">Aanmeldingsactiviteiten van gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="afb0b-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="afb0b-168">In de informatie die wordt aangeboden in het rapport over aanmeldingsactiviteiten van gebruikers, vindt u antwoord op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="afb0b-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="afb0b-169">Wat is het aanmeldingspatroon van een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="afb0b-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="afb0b-170">Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?</span><span class="sxs-lookup"><span data-stu-id="afb0b-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="afb0b-171">Wat is de status van deze aanmeldingen?</span><span class="sxs-lookup"><span data-stu-id="afb0b-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="afb0b-172">Uw beginpunt voor deze gegevens is de aanmeldingsgrafiek van gebruikers in het gedeelte **Overzicht** onder **Gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="afb0b-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="afb0b-173">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/45.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-174">In de aanmeldingsgrafiek van gebruikers ziet u alle aanmeldingen van alle gebruikers gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="afb0b-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="afb0b-175">De standaard ingestelde periode is 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="afb0b-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="afb0b-176">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/46.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-177">Als u in de aanmeldingsgrafiek op een dag klikt, ziet u een gedetailleerd overzicht van de aanmeldingsactiviteiten voor die dag.</span><span class="sxs-lookup"><span data-stu-id="afb0b-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="afb0b-178">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/41.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-179">Elke rij in de lijst met aanmeldingsactiviteiten bevat gedetailleerde informatie over de geselecteerde aanmelding, zoals:</span><span class="sxs-lookup"><span data-stu-id="afb0b-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="afb0b-180">Wie heeft zich aangemeld?</span><span class="sxs-lookup"><span data-stu-id="afb0b-180">Who has signed in?</span></span>
* <span data-ttu-id="afb0b-181">Wat was de gerelateerde UPN?</span><span class="sxs-lookup"><span data-stu-id="afb0b-181">What was the related UPN?</span></span>
* <span data-ttu-id="afb0b-182">Welke toepassing was het aanmeldingsdoel?</span><span class="sxs-lookup"><span data-stu-id="afb0b-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="afb0b-183">Wat is het IP-adres van de persoon die zich heeft aangemeld?</span><span class="sxs-lookup"><span data-stu-id="afb0b-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="afb0b-184">Wat is de status van de aanmelding?</span><span class="sxs-lookup"><span data-stu-id="afb0b-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="afb0b-185">Met de optie **Aanmeldingen** krijgt u een volledig overzicht van alle gebruikersaanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="afb0b-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="afb0b-186">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/51.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="afb0b-187">Het gebruik van beheerde toepassingen</span><span class="sxs-lookup"><span data-stu-id="afb0b-187">Usage of managed applications</span></span>

<span data-ttu-id="afb0b-188">Met een toepassingsgerichte weergave van uw aanmeldingsgegevens kunt u antwoord vinden op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="afb0b-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="afb0b-189">Wie gebruikt mijn toepassingen?</span><span class="sxs-lookup"><span data-stu-id="afb0b-189">Who is using my applications?</span></span>
* <span data-ttu-id="afb0b-190">Wat zijn de drie meest gebruikte toepassingen in uw organisatie?</span><span class="sxs-lookup"><span data-stu-id="afb0b-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="afb0b-191">Ik heb onlangs een toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="afb0b-191">I have recently rolled out an application.</span></span> <span data-ttu-id="afb0b-192">Hoe gaat het ermee?</span><span class="sxs-lookup"><span data-stu-id="afb0b-192">How is it doing?</span></span>

<span data-ttu-id="afb0b-193">Uw beginpunt voor deze gegevens is het overzicht van de drie populairste toepassingen in uw organisatie volgens het rapport van de laatste 30 dagen. Het overzicht vindt u in het gedeelte **Overzicht** onder **Bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="afb0b-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="afb0b-194">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/64.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-195">In de grafiek over appgebruik staat een wekelijks overzicht van alle aanmeldingen bij de drie populairste toepassingen gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="afb0b-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="afb0b-196">De standaard ingestelde periode is 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="afb0b-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="afb0b-197">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/47.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="afb0b-198">Als u wilt, kunt u de focus instellen op een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="afb0b-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="afb0b-199">![Rapportage](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Rapportage")</span><span class="sxs-lookup"><span data-stu-id="afb0b-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="afb0b-200">Als u op een dag in de appgebruikgrafiek klikt, ziet u een gedetailleerd overzicht van de aanmeldactiviteiten.</span><span class="sxs-lookup"><span data-stu-id="afb0b-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="afb0b-201">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/48.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="afb0b-202">Met de optie **Aanmeldingen** krijgt u een volledig overzicht van alle aanmeldingsgebeurtenissen voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="afb0b-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="afb0b-203">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/49.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="afb0b-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="afb0b-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="afb0b-204">Next steps</span></span>

<span data-ttu-id="afb0b-205">Als u meer wilt weten over foutcodes voor aanmeldingsactiviteiten, raadpleegt u [Foutcodes voor aanmeldactiviteitenrapporten in Azure Active Directory Portal](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="afb0b-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

