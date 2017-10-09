---
title: Active Directory-rapportage aaaAzure | Microsoft Docs
description: Biedt een algemeen overzicht van Azure Active Directory-rapportage.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="11df2-103">Azure Active Directory-rapportage</span><span class="sxs-lookup"><span data-stu-id="11df2-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="11df2-104">Met Azure Active Directory-rapportage krijgt u inzicht in hoe uw omgeving presteert.</span><span class="sxs-lookup"><span data-stu-id="11df2-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="11df2-105">Hallo opgegeven gegevens kunt u:</span><span class="sxs-lookup"><span data-stu-id="11df2-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="11df2-106">Vaststellen hoe uw apps en services door uw gebruikers worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="11df2-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="11df2-107">Potentiële risico's die invloed hebben op Hallo status van uw omgeving detecteren</span><span class="sxs-lookup"><span data-stu-id="11df2-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="11df2-108">Problemen oplossen waardoor uw gebruikers hun werk niet kunnen doen</span><span class="sxs-lookup"><span data-stu-id="11df2-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="11df2-109">Er is een Hallo reporting architectuur afhankelijk van de twee belangrijkste stijlen:</span><span class="sxs-lookup"><span data-stu-id="11df2-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="11df2-110">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="11df2-110">Security reports</span></span>
- <span data-ttu-id="11df2-111">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="11df2-111">Activity reports</span></span>

![Rapportage](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="11df2-113">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="11df2-113">Security reports</span></span>

<span data-ttu-id="11df2-114">Hallo beveiligingsrapporten in Azure Active Directory kunnen u tooprotect identiteiten van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="11df2-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="11df2-115">Er zijn in Azure Active Directory twee soorten beveiligingsrapporten:</span><span class="sxs-lookup"><span data-stu-id="11df2-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="11df2-116">**Gebruikers die zijn gemarkeerd voor risico** - van Hallo [gebruikers gemarkeerd voor risico beveiligingsrapport](active-directory-reporting-security-user-at-risk.md), u krijgt u een overzicht van gebruikersaccounts die mogelijk zijn aangetast.</span><span class="sxs-lookup"><span data-stu-id="11df2-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="11df2-117">**Riskant aanmeldingen** - Hello [beveiligingsrapport voor riskante aanmelden](active-directory-reporting-security-risky-sign-ins.md), u een indicator voor aanmeldpogingen die mogelijk zijn uitgevoerd door iemand die niet Hallo rechtmatige eigenaar van een gebruikersaccount niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="11df2-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="11df2-118">**Welke Azure AD-licentie hebt u een beveiligingsrapport tooaccess nodig?**</span><span class="sxs-lookup"><span data-stu-id="11df2-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="11df2-119">Alle edities van Azure Active Directory bieden rapporten over gebruikers voor wie wordt aangegeven dat ze risico lopen en rapporten over riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="11df2-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="11df2-120">Hallo-niveau van rapportgranulatie is echter van Hallo edities:</span><span class="sxs-lookup"><span data-stu-id="11df2-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="11df2-121">In Hallo **edities Azure Active Directory gratis en Basic**, u al een lijst met gebruikers die zijn gemarkeerd voor risico en riskant aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="11df2-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="11df2-122">Hallo **Azure Active Directory Premium 1** edition wordt dit model uitgebreid doordat ook u tooexamine aantal Hallo onderliggende risico's die zijn gedetecteerd voor elk rapport.</span><span class="sxs-lookup"><span data-stu-id="11df2-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="11df2-123">Hallo **Azure Active Directory Premium 2** editie biedt u Hello meest gedetailleerde informatie weer over Hallo onderliggende risicogebeurtenissen en ook kunt u beveiligingsbeleid tooconfigure die automatisch tooconfigured reageren risiconiveaus.</span><span class="sxs-lookup"><span data-stu-id="11df2-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="11df2-124">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="11df2-124">Activity reports</span></span>

<span data-ttu-id="11df2-125">Er zijn in Azure Active Directory twee soorten activiteitsrapporten:</span><span class="sxs-lookup"><span data-stu-id="11df2-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="11df2-126">**Controlelogboeken** - hello [auditlogboeken activiteitenrapport](active-directory-reporting-activity-audit-logs.md) biedt u toegang toohello geschiedenis van elke taak uit te voeren in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="11df2-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="11df2-127">**Aanmeldingen** - Hello [aanmeldingen activiteitenrapport](active-directory-reporting-activity-sign-ins.md), kunt u bepalen, wie Hallo-taken die zijn gerapporteerd door Hallo audit logboeken rapport is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="11df2-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="11df2-128">Hallo **auditlogboeken rapport** biedt u records van het systeemactiviteiten voor naleving.</span><span class="sxs-lookup"><span data-stu-id="11df2-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="11df2-129">Onder andere opgegeven Hallo gegevens kunt u tooaddress algemene scenario's, zoals:</span><span class="sxs-lookup"><span data-stu-id="11df2-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="11df2-130">Iemand in mijn tenants heeft toegang tooan administratorgroep.</span><span class="sxs-lookup"><span data-stu-id="11df2-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="11df2-131">Wie heeft diegene toegang verleend?</span><span class="sxs-lookup"><span data-stu-id="11df2-131">Who gave them access?</span></span> 

- <span data-ttu-id="11df2-132">Ik wil tooknow Hallo lijst met gebruikers die zich in een specifieke app sinds ik onlangs vrijgegeven Hallo app en wilt tooknow als het goed actief</span><span class="sxs-lookup"><span data-stu-id="11df2-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="11df2-133">Ik wil tooknow hoeveel wachtwoord opnieuw instellen van plaatsvinden in mijn tenants</span><span class="sxs-lookup"><span data-stu-id="11df2-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="11df2-134">**Welke Azure AD-licentie hebt u tooaccess Hallo controlerapport logboeken nodig?**</span><span class="sxs-lookup"><span data-stu-id="11df2-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="11df2-135">Hallo-controlerapport Logboeken is beschikbaar voor functies waarvoor u licenties hebt.</span><span class="sxs-lookup"><span data-stu-id="11df2-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="11df2-136">Als u een licentie voor een specifieke functie hebt, hebt u ook toegang toohello controle-logboekinformatie voor het.</span><span class="sxs-lookup"><span data-stu-id="11df2-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="11df2-137">Zie voor meer informatie **algemeen beschikbaar functies van Hallo vrije, Basic en Premium-edities vergelijken** in [Azure Active Directory-functies en mogelijkheden](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="11df2-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="11df2-138">Hallo **aanmeldingen activiteitenrapport** schakelt tootoofind beantwoordt tooquestions, zoals:</span><span class="sxs-lookup"><span data-stu-id="11df2-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="11df2-139">Wat is Hallo aanmelden patroon van een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="11df2-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="11df2-140">Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?</span><span class="sxs-lookup"><span data-stu-id="11df2-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="11df2-141">Wat is de status van deze aanmeldingen Hallo?</span><span class="sxs-lookup"><span data-stu-id="11df2-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="11df2-142">**Welke Azure AD-licentie wilt u moet tooaccess Hallo aanmeldingen activiteitenrapport?**</span><span class="sxs-lookup"><span data-stu-id="11df2-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="11df2-143">tooaccess Hallo activiteitenrapport aanmeldingen, uw tenant moet beschikken over een Azure AD Premium-licentie gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="11df2-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="11df2-144">Toegang op programmeerniveau</span><span class="sxs-lookup"><span data-stu-id="11df2-144">Programmatic access</span></span>

<span data-ttu-id="11df2-145">In de gebruikersinterface voor toevoeging toohello, rapportage van Azure Active Directory biedt u ook met [toegang op programmeerniveau](active-directory-reporting-api-getting-started-azure-portal.md) toohello rapportgegevens.</span><span class="sxs-lookup"><span data-stu-id="11df2-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="11df2-146">Hallo-gegevens van deze rapporten kunnen zeer nuttig tooyour toepassingen, zoals de SIEM-systemen, controle en hulpprogramma's voor bedrijfsinformatie worden.</span><span class="sxs-lookup"><span data-stu-id="11df2-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="11df2-147">Hello Azure AD rapportage-API's bieden toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="11df2-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="11df2-148">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="11df2-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="11df2-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11df2-149">Next steps</span></span>

<span data-ttu-id="11df2-150">Als u meer informatie over Hallo tooknow verschillende rapporttypen in Azure Active Directory wilt, Zie:</span><span class="sxs-lookup"><span data-stu-id="11df2-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="11df2-151">Rapport voor Gebruikers voor wie wordt aangegeven dat ze risico lopen</span><span class="sxs-lookup"><span data-stu-id="11df2-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="11df2-152">Rapport voor riskante aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="11df2-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="11df2-153">Rapport voor audittrails</span><span class="sxs-lookup"><span data-stu-id="11df2-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="11df2-154">Rapport voor aanmeldlogboeken</span><span class="sxs-lookup"><span data-stu-id="11df2-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="11df2-155">Als u meer over het openen van Hallo Hallo rapportagegegevens Hallo rapportage-API met tooknow wilt, Zie:</span><span class="sxs-lookup"><span data-stu-id="11df2-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="11df2-156">Aan de slag met Azure Active Directory-rapportage API Hallo</span><span class="sxs-lookup"><span data-stu-id="11df2-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png