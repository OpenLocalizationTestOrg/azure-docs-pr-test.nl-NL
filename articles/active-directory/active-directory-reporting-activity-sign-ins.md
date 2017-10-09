---
title: activiteit aaaSign in rapporten in Azure Active Directory-beheerportal Hallo | Microsoft Docs
description: Inleiding activiteit toosign in rapporten in hello Azure Active Directory-portal
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
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="c23db-103">Rapporten in Azure Active Directory-beheerportal Hallo aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="c23db-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="c23db-104">Met Azure Active Directory (Azure AD) rapportage in Hallo [Azure-portal](https://portal.azure.com), krijgt u Hallo-informatie die u nodig hebt toodetermine hoe uw omgeving doet.</span><span class="sxs-lookup"><span data-stu-id="c23db-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="c23db-105">Hallo-architectuur in Azure Active Directory reporting bestaat uit Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="c23db-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="c23db-106">**Activiteit**</span><span class="sxs-lookup"><span data-stu-id="c23db-106">**Activity**</span></span> 
    - <span data-ttu-id="c23db-107">**Aanmelden activiteiten** – informatie over het gebruik van Hallo van beheerde toepassingen en gebruikersactiviteiten aanmelden</span><span class="sxs-lookup"><span data-stu-id="c23db-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="c23db-108">**Controlelogboeken**: informatie over systeemactiviteit van gebruikers, groepsbeheer, uw beheerde toepassingen en directory-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c23db-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="c23db-109">**Beveiliging**</span><span class="sxs-lookup"><span data-stu-id="c23db-109">**Security**</span></span> 
    - <span data-ttu-id="c23db-110">**Riskant aanmeldingen** -een riskante aanmelden is een indicator voor een aanmeldingspoging die mogelijk zijn uitgevoerd door iemand die niet Hallo legitieme eigenaar van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="c23db-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="c23db-111">Zie Riskante aanmeldingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c23db-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="c23db-112">**Gebruikers van wie wordt aangegeven dat ze risico lopen** - Een riskante gebruiker is een indicator van een gebruikersaccount dat mogelijk is aangetast.</span><span class="sxs-lookup"><span data-stu-id="c23db-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="c23db-113">Zie Gebruikers van wie wordt aangegeven dat ze risico lopen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c23db-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="c23db-114">In dit onderwerp biedt een overzicht van Hallo aanmelden activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c23db-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="c23db-115">Vereiste</span><span class="sxs-lookup"><span data-stu-id="c23db-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="c23db-116">Wie toegang heeft tot Hallo gegevens?</span><span class="sxs-lookup"><span data-stu-id="c23db-116">Who can access hello data?</span></span>
* <span data-ttu-id="c23db-117">Gebruikers met de rol beheerder beveiliging of beveiliging Reader Hallo</span><span class="sxs-lookup"><span data-stu-id="c23db-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="c23db-118">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="c23db-118">Global Admins</span></span>
* <span data-ttu-id="c23db-119">Alle gebruiker (niet-beheerders) hebben toegang tot hun eigen aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="c23db-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="c23db-120">Welke Azure AD-licentie moet u de aanmeldingsactiviteiten tooaccess?</span><span class="sxs-lookup"><span data-stu-id="c23db-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="c23db-121">Uw tenant moet beschikken over een Azure AD Premium-licentie gekoppeld toosee Hallo alles op aanmeldingsactiviteiten rapport</span><span class="sxs-lookup"><span data-stu-id="c23db-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="c23db-122">Aanmeldactiviteiten</span><span class="sxs-lookup"><span data-stu-id="c23db-122">Signs-in activities</span></span>

<span data-ttu-id="c23db-123">Hallo informatie verstrekt door de gebruiker aanmelden rapport hello, ziet u de antwoorden tooquestions zoals:</span><span class="sxs-lookup"><span data-stu-id="c23db-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="c23db-124">Wat is Hallo aanmelden patroon van een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="c23db-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="c23db-125">Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?</span><span class="sxs-lookup"><span data-stu-id="c23db-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="c23db-126">Wat is de status van deze aanmeldingen Hallo?</span><span class="sxs-lookup"><span data-stu-id="c23db-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="c23db-127">Uw eerste vermelding punt tooall aanmelden activiteiten gegevens **aanmeldingen** in Hallo activiteit sectie van **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="c23db-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="c23db-128">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/61.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="c23db-129">Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:</span><span class="sxs-lookup"><span data-stu-id="c23db-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="c23db-130">Hallo gerelateerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="c23db-130">hello related user</span></span>
- <span data-ttu-id="c23db-131">Hallo toepassing hello gebruiker is aangemeld bij</span><span class="sxs-lookup"><span data-stu-id="c23db-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="c23db-132">Hallo-in status</span><span class="sxs-lookup"><span data-stu-id="c23db-132">hello sign-in status</span></span>
- <span data-ttu-id="c23db-133">tijd van aanmelden Hallo</span><span class="sxs-lookup"><span data-stu-id="c23db-133">hello sign-in time</span></span>

<span data-ttu-id="c23db-134">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/41.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-135">U kunt de lijstweergave Hallo aanpassen door te klikken op **kolommen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="c23db-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="c23db-136">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/19.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-137">Dit kunt u aanvullende velden toodisplay of verwijderen van de velden die al worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c23db-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="c23db-138">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/42.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-139">Door te klikken op een item in de lijstweergave hello, moet u alle beschikbare details over het ophalen.</span><span class="sxs-lookup"><span data-stu-id="c23db-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="c23db-140">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/43.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="c23db-141">Aanmeldingsactiviteiten filteren</span><span class="sxs-lookup"><span data-stu-id="c23db-141">Filtering sign-in activities</span></span>

<span data-ttu-id="c23db-142">toonarrow omlaag Hallo tooa gegevensniveau dat geldt voor u, kunt u Hallo aanmeldingen gegevens filteren met behulp van de volgende velden Hallo gerapporteerd:</span><span class="sxs-lookup"><span data-stu-id="c23db-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="c23db-143">Tijdsinterval</span><span class="sxs-lookup"><span data-stu-id="c23db-143">Time interval</span></span>
- <span data-ttu-id="c23db-144">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="c23db-144">User</span></span>
- <span data-ttu-id="c23db-145">Toepassing</span><span class="sxs-lookup"><span data-stu-id="c23db-145">Application</span></span>
- <span data-ttu-id="c23db-146">Client</span><span class="sxs-lookup"><span data-stu-id="c23db-146">Client</span></span>
- <span data-ttu-id="c23db-147">Aanmeldingsstatus</span><span class="sxs-lookup"><span data-stu-id="c23db-147">Sign-in status</span></span>

<span data-ttu-id="c23db-148">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/44.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="c23db-149">Hallo **tijdsinterval** filter schakelt tooyou toodefine een tijdsspanne voor Hallo gegevens geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c23db-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="c23db-150">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="c23db-150">Possible values are:</span></span>

- <span data-ttu-id="c23db-151">1 maand</span><span class="sxs-lookup"><span data-stu-id="c23db-151">1 month</span></span>
- <span data-ttu-id="c23db-152">7 dagen</span><span class="sxs-lookup"><span data-stu-id="c23db-152">7 days</span></span>
- <span data-ttu-id="c23db-153">24 uur</span><span class="sxs-lookup"><span data-stu-id="c23db-153">24 hours</span></span>
- <span data-ttu-id="c23db-154">Aangepast telefoonnummer</span><span class="sxs-lookup"><span data-stu-id="c23db-154">Custom</span></span>

<span data-ttu-id="c23db-155">Wanneer u een aangepast tijdsbestek selecteert, kunt u een begintijd en eindtijd configureren.</span><span class="sxs-lookup"><span data-stu-id="c23db-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="c23db-156">Hallo **gebruiker** filter kunt u toospecify Hallo naam of het Hallo UPN (user Principal name) van Hallo-gebruiker die u interesseren.</span><span class="sxs-lookup"><span data-stu-id="c23db-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="c23db-157">Hallo **toepassing** filter kunt u de naam van de toospecify Hallo van Hallo-toepassing die u interesseren.</span><span class="sxs-lookup"><span data-stu-id="c23db-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="c23db-158">Hallo **client** filter kunt u toospecify informatie over het Hallo-apparaat die u interesseren.</span><span class="sxs-lookup"><span data-stu-id="c23db-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="c23db-159">Hallo **aanmeldingsstatus** filter kunt u tooselect Hallo filter te volgen:</span><span class="sxs-lookup"><span data-stu-id="c23db-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="c23db-160">Alle</span><span class="sxs-lookup"><span data-stu-id="c23db-160">All</span></span>
- <span data-ttu-id="c23db-161">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="c23db-161">Success</span></span>
- <span data-ttu-id="c23db-162">Fout</span><span class="sxs-lookup"><span data-stu-id="c23db-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="c23db-163">Snelkoppelingen voor aanmeldingsactiviteiten</span><span class="sxs-lookup"><span data-stu-id="c23db-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="c23db-164">Bovendien tooAzure Active Directory, hello Azure-portal biedt twee extra post punten toosign in activiteiten gegevens:</span><span class="sxs-lookup"><span data-stu-id="c23db-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="c23db-165">Gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="c23db-165">Users and groups</span></span>
- <span data-ttu-id="c23db-166">Bedrijfstoepassingen</span><span class="sxs-lookup"><span data-stu-id="c23db-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="c23db-167">Aanmeldingsactiviteiten van gebruikers en groepen</span><span class="sxs-lookup"><span data-stu-id="c23db-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="c23db-168">Hallo informatie verstrekt door de gebruiker aanmelden rapport hello, ziet u de antwoorden tooquestions zoals:</span><span class="sxs-lookup"><span data-stu-id="c23db-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="c23db-169">Wat is Hallo aanmelden patroon van een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="c23db-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="c23db-170">Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?</span><span class="sxs-lookup"><span data-stu-id="c23db-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="c23db-171">Wat is de status van deze aanmeldingen Hallo?</span><span class="sxs-lookup"><span data-stu-id="c23db-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="c23db-172">Punt toothis postgegevens is gebruiker aanmelden grafiek Hallo in Hallo **overzicht** onder sectie **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="c23db-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="c23db-173">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/45.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-174">Hallo gebruiker aanmelden grafiek toont wekelijkse aggregaties van de registratie-modules voor alle gebruikers in een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="c23db-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="c23db-175">Hallo-standaardwaarde voor Hallo is periode 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="c23db-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="c23db-176">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/46.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-177">Als u op een dag in Hallo aanmelden grafiek klikt, krijgt u een gedetailleerde lijst met Hallo aanmelden activiteiten voor deze dag.</span><span class="sxs-lookup"><span data-stu-id="c23db-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="c23db-178">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/41.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-179">Elke rij in Hallo aanmelden activiteiten lijst kunt die u gedetailleerde informatie over Hallo geselecteerd aanmelden zoals Hallo:</span><span class="sxs-lookup"><span data-stu-id="c23db-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="c23db-180">Wie heeft zich aangemeld?</span><span class="sxs-lookup"><span data-stu-id="c23db-180">Who has signed in?</span></span>
* <span data-ttu-id="c23db-181">Wat was Hallo gerelateerde UPN?</span><span class="sxs-lookup"><span data-stu-id="c23db-181">What was hello related UPN?</span></span>
* <span data-ttu-id="c23db-182">Welke toepassing hello doel van de aanmeldingspagina Hallo was?</span><span class="sxs-lookup"><span data-stu-id="c23db-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="c23db-183">Wat is Hallo IP-adres van de aanmeldingspagina Hallo?</span><span class="sxs-lookup"><span data-stu-id="c23db-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="c23db-184">Wat is Hallo status van Hallo aanmelden?</span><span class="sxs-lookup"><span data-stu-id="c23db-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="c23db-185">Hallo **aanmeldingen** optie biedt u een volledig overzicht van alle gebruikersaanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="c23db-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="c23db-186">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/51.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="c23db-187">Het gebruik van beheerde toepassingen</span><span class="sxs-lookup"><span data-stu-id="c23db-187">Usage of managed applications</span></span>

<span data-ttu-id="c23db-188">Met een toepassingsgerichte weergave van uw aanmeldingsgegevens kunt u antwoord vinden op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="c23db-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="c23db-189">Wie gebruikt mijn toepassingen?</span><span class="sxs-lookup"><span data-stu-id="c23db-189">Who is using my applications?</span></span>
* <span data-ttu-id="c23db-190">Wat zijn de eerste Hallo 3 toepassingen in uw organisatie?</span><span class="sxs-lookup"><span data-stu-id="c23db-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="c23db-191">Ik heb onlangs een toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c23db-191">I have recently rolled out an application.</span></span> <span data-ttu-id="c23db-192">Hoe gaat het ermee?</span><span class="sxs-lookup"><span data-stu-id="c23db-192">How is it doing?</span></span>

<span data-ttu-id="c23db-193">Punt toothis postgegevens is Hallo eerste 3 toepassingen in uw organisatie binnen de laatste 30 dagen rapport in Hallo Hallo **overzicht** onder sectie **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="c23db-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="c23db-194">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/64.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-195">Hallo-app-gebruik grafiek wekelijkse aggregaties van aanmeldingen voor uw top-3-toepassingen in een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="c23db-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="c23db-196">Hallo-standaardwaarde voor Hallo is periode 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="c23db-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="c23db-197">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/47.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="c23db-198">Als u wilt, kunt u Hallo focus instellen op een specifieke toepassing.</span><span class="sxs-lookup"><span data-stu-id="c23db-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="c23db-199">![Rapportage](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Rapportage")</span><span class="sxs-lookup"><span data-stu-id="c23db-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="c23db-200">Als u op een dag in Hallo app gebruiksgrafiek klikt, krijgt u een gedetailleerde lijst met Hallo aanmelden activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c23db-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="c23db-201">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/48.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="c23db-202">Hallo **aanmeldingen** optie biedt u een volledig overzicht van alle gebeurtenissen aanmelden tooyour toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c23db-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="c23db-203">![Aanmeldingsactiviteit](./media/active-directory-reporting-activity-sign-ins/49.png "Aanmeldingsactiviteit")</span><span class="sxs-lookup"><span data-stu-id="c23db-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="c23db-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c23db-204">Next steps</span></span>

<span data-ttu-id="c23db-205">Als u meer informatie over foutcodes aanmeldingsactiviteiten tooknow wilt, raadpleegt u Hallo [aanmelden activiteit rapport-foutcodes in Azure Active Directory-beheerportal Hallo](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="c23db-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

