---
title: Azure Active Directory-rapportage | Microsoft Docs
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
ms.openlocfilehash: 738c8f4a56586b87f03973ec258b0a3023affa60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="09668-103">Azure Active Directory-rapportage</span><span class="sxs-lookup"><span data-stu-id="09668-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="09668-104">Met Azure Active Directory-rapportage krijgt u inzicht in hoe uw omgeving presteert.</span><span class="sxs-lookup"><span data-stu-id="09668-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="09668-105">Met de gegevens kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="09668-105">The provided data enables you to:</span></span>

- <span data-ttu-id="09668-106">Vaststellen hoe uw apps en services door uw gebruikers worden gebruikt</span><span class="sxs-lookup"><span data-stu-id="09668-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="09668-107">Potentiële risico's detecteren die invloed hebben op de status van uw omgeving</span><span class="sxs-lookup"><span data-stu-id="09668-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="09668-108">Problemen oplossen waardoor uw gebruikers hun werk niet kunnen doen</span><span class="sxs-lookup"><span data-stu-id="09668-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="09668-109">De rapportagearchitectuur is afhankelijk van twee belangrijke zaken:</span><span class="sxs-lookup"><span data-stu-id="09668-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="09668-110">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="09668-110">Security reports</span></span>
- <span data-ttu-id="09668-111">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="09668-111">Activity reports</span></span>

![Rapportage](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="09668-113">Beveiligingsrapporten</span><span class="sxs-lookup"><span data-stu-id="09668-113">Security reports</span></span>

<span data-ttu-id="09668-114">Met de beveiligingsrapporten in Azure Active Directory kunt u de identiteiten van uw organisatie beschermen.</span><span class="sxs-lookup"><span data-stu-id="09668-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="09668-115">Er zijn in Azure Active Directory twee soorten beveiligingsrapporten:</span><span class="sxs-lookup"><span data-stu-id="09668-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="09668-116">**Gebruikers voor wie wordt aangegeven dat ze risico lopen**: in het rapport [Gebruikers voor wie wordt aangegeven dat ze risico lopen](active-directory-reporting-security-user-at-risk.md) krijgt u een overzicht van gebruikersaccounts die mogelijk zijn aangetast.</span><span class="sxs-lookup"><span data-stu-id="09668-116">**Users flagged for risk** - From the [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="09668-117">**Riskante aanmeldingen**: in het beveiligingsrapport [Riskante aanmeldingen](active-directory-reporting-security-risky-sign-ins.md) krijgt u een idee van aanmeldingspogingen die mogelijk zijn uitgevoerd door iemand die geen rechtmatige eigenaar van een gebruikersaccount is.</span><span class="sxs-lookup"><span data-stu-id="09668-117">**Risky sign-ins** - With the [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="09668-118">**Welke Azure AD-licentie heb ik nodig voor toegang tot een beveiligingsrapport?**</span><span class="sxs-lookup"><span data-stu-id="09668-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="09668-119">Alle edities van Azure Active Directory bieden rapporten over gebruikers voor wie wordt aangegeven dat ze risico lopen en rapporten over riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="09668-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="09668-120">Het detailniveau van rapporten verschilt wel per editie:</span><span class="sxs-lookup"><span data-stu-id="09668-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="09668-121">In de edities **Azure Active Directory Free en Basic** hebt u toegang tot een lijst die gebruikers bevat voor wie wordt aangegeven dat ze risico lopen, evenals riskante aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="09668-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="09668-122">De editie **Azure Active Directory Premium 1** bevat een uitgebreider model waarmee u ook bepaalde onderliggende risicogebeurtenissen kunt onderzoeken die voor elk rapport zijn gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="09668-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="09668-123">De editie **Azure Active Directory Premium 2** biedt u de meest gedetailleerde informatie over de onderliggende risicogebeurtenissen. Deze editie stelt u ook in staat beveiligingsbeleidsregels te configureren die automatisch op de geconfigureerde risiconiveaus reageren.</span><span class="sxs-lookup"><span data-stu-id="09668-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="09668-124">Activiteitsrapporten</span><span class="sxs-lookup"><span data-stu-id="09668-124">Activity reports</span></span>

<span data-ttu-id="09668-125">Er zijn in Azure Active Directory twee soorten activiteitsrapporten:</span><span class="sxs-lookup"><span data-stu-id="09668-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="09668-126">**Audittrails**: het [activiteitenrapport voor audittrails](active-directory-reporting-activity-audit-logs.md) biedt u toegang tot de geschiedenis van elke taak die in uw tenant is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="09668-126">**Audit logs** - The [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="09668-127">**Aanmeldingen**: met het [activiteitenrapport voor aanmeldingen](active-directory-reporting-activity-sign-ins.md) kunt u bepalen wie de taken heeft uitgevoerd die in het audittrailrapport zijn gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="09668-127">**Sign-ins** -  With the [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="09668-128">De **audittrailrapporten** bieden records van systeemactiviteiten in het kader van naleving.</span><span class="sxs-lookup"><span data-stu-id="09668-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="09668-129">Met de geleverde gegevens kunt u onder andere de volgende veelvoorkomende vragen beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="09668-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="09668-130">Iemand in mijn tenant heeft toegang gekregen tot een beheerdersgroep.</span><span class="sxs-lookup"><span data-stu-id="09668-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="09668-131">Wie heeft diegene toegang verleend?</span><span class="sxs-lookup"><span data-stu-id="09668-131">Who gave them access?</span></span> 

- <span data-ttu-id="09668-132">Ik wil een lijst weergeven met gebruikers die zich in een specifieke app hebben aangemeld sinds ik de app onlangs heb toegevoegd en wil weten of de app het goed doet</span><span class="sxs-lookup"><span data-stu-id="09668-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="09668-133">Ik wil weten hoe vaak er in mijn tenant een wachtwoord opnieuw is ingesteld</span><span class="sxs-lookup"><span data-stu-id="09668-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="09668-134">**Welke Azure AD-licentie heb ik nodig voor toegang tot audittrailrapporten?**</span><span class="sxs-lookup"><span data-stu-id="09668-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="09668-135">Het audittrailrapport is beschikbaar voor functies waarvoor u licenties hebt.</span><span class="sxs-lookup"><span data-stu-id="09668-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="09668-136">Als u een licentie voor een specifieke functie hebt, hebt u ook toegang tot de audittrailgegevens hiervan.</span><span class="sxs-lookup"><span data-stu-id="09668-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="09668-137">Zie **Comparing generally available features of the Free, Basic, and Premium editions** (Algemeen beschikbare functies van de Free-, Basic- en Premium-edities vergelijken) in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features) (Functies en mogelijkheden van Azure Active Directory) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="09668-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="09668-138">Het **aanmeldactiviteitenrapport** helpt u antwoorden te vinden op vragen zoals:</span><span class="sxs-lookup"><span data-stu-id="09668-138">The **sign-ins activity report** enables to to find answers to questions such as:</span></span>

- <span data-ttu-id="09668-139">Wat is het aanmeldingspatroon van een gebruiker?</span><span class="sxs-lookup"><span data-stu-id="09668-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="09668-140">Hoeveel keer hebben gebruikers zich aangemeld gedurende een week?</span><span class="sxs-lookup"><span data-stu-id="09668-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="09668-141">Wat is de status van deze aanmeldingen?</span><span class="sxs-lookup"><span data-stu-id="09668-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="09668-142">**Welke Azure AD-licentie heb ik nodig voor toegang tot het aanmeldactiviteitenrapport?**</span><span class="sxs-lookup"><span data-stu-id="09668-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="09668-143">Uw tenant moet beschikken over een Azure AD Premium-licentie om het rapport met aanmeldactiviteiten te kunnen openen.</span><span class="sxs-lookup"><span data-stu-id="09668-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="09668-144">Toegang op programmeerniveau</span><span class="sxs-lookup"><span data-stu-id="09668-144">Programmatic access</span></span>

<span data-ttu-id="09668-145">De rapportage van Azure Active Directory biedt u naast de gebruikersinterface ook [toegang op programmeerniveau](active-directory-reporting-api-getting-started-azure-portal.md) tot de rapportagegegevens.</span><span class="sxs-lookup"><span data-stu-id="09668-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) to the reporting data.</span></span> <span data-ttu-id="09668-146">De gegevens van deze rapporten kunnen zeer nuttig zijn voor uw toepassingen, zoals SIEM-systemen, audit- en business intelligence-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="09668-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="09668-147">De API's van Azure AD Reporting bieden toegang tot de gegevens op programmeerniveau via een set op REST-gebaseerde API's.</span><span class="sxs-lookup"><span data-stu-id="09668-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="09668-148">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="09668-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="09668-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09668-149">Next steps</span></span>

<span data-ttu-id="09668-150">Als u meer wilt weten over de verschillende soorten rapporten in Azure Active Directory, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="09668-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="09668-151">Rapport voor Gebruikers voor wie wordt aangegeven dat ze risico lopen</span><span class="sxs-lookup"><span data-stu-id="09668-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="09668-152">Rapport voor riskante aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="09668-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="09668-153">Rapport voor audittrails</span><span class="sxs-lookup"><span data-stu-id="09668-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="09668-154">Rapport voor aanmeldlogboeken</span><span class="sxs-lookup"><span data-stu-id="09668-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="09668-155">Als u meer weten wilt over het openen van de rapportagegegevens met de rapportage-API, raadpleegt u:</span><span class="sxs-lookup"><span data-stu-id="09668-155">If you want to know more about accessing the the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="09668-156">Aan de slag met de Azure Active Directory Reporting-API</span><span class="sxs-lookup"><span data-stu-id="09668-156">Getting started with the Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png