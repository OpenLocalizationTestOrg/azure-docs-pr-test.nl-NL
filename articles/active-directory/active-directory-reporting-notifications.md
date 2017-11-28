---
title: aaaAzure Active Directory-rapportage meldingen
description: Hoe toouse reporting meldingen van de Azure Active Directory voor verdacht Hallo modules.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="6eec1-103">Azure Active Directory-rapportage meldingen</span><span class="sxs-lookup"><span data-stu-id="6eec1-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="6eec1-104">Welke rapporten genereren e-mailmeldingen</span><span class="sxs-lookup"><span data-stu-id="6eec1-104">What reports generate email notifications</span></span>
<span data-ttu-id="6eec1-105">Op dit moment alleen Hallo onregelmatige aanmelding in activiteit rapport triggers e-mailmeldingen.</span><span class="sxs-lookup"><span data-stu-id="6eec1-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="6eec1-106">Wat is een 'onregelmatige aanmelden'?</span><span class="sxs-lookup"><span data-stu-id="6eec1-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="6eec1-107">Onregelmatige aanmeldingen zijn bestanden die zijn geïdentificeerd door onze machine learning-algoritmen, op basis van een 'onmogelijke reis' voorwaarde gecombineerd met een afwijkende locatie aanmelden en het apparaat Hallo.</span><span class="sxs-lookup"><span data-stu-id="6eec1-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="6eec1-108">Dit kan erop wijzen dat een hacker is probeert toosign in dit account wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6eec1-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="6eec1-109">Wie Hallo e-mailmeldingen ontvangen?</span><span class="sxs-lookup"><span data-stu-id="6eec1-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="6eec1-110">Hallo-e-mailbericht verzonden tooall globale beheerders die zijn toegewezen in een Active Directory Premium-licentie.</span><span class="sxs-lookup"><span data-stu-id="6eec1-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="6eec1-111">tooensure die wordt bezorgd, we verzenden toohello admins alternatief e-mailadres ook.</span><span class="sxs-lookup"><span data-stu-id="6eec1-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="6eec1-112">Beheerders moeten bevatten aad-alerts-noreply@mail.windowsazure.com in hun lijst met veilige afzenders zodat er geen Hallo e zijn gemist.</span><span class="sxs-lookup"><span data-stu-id="6eec1-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="6eec1-113">Hoe vaak worden deze e-mailberichten verzonden?</span><span class="sxs-lookup"><span data-stu-id="6eec1-113">How often are these emails sent?</span></span>
<span data-ttu-id="6eec1-114">Hallo-e-mailbericht wordt verzonden als de 10 nieuwe onregelmatige aanmelden activiteiten plaatsvinden in Hallo afgelopen 30 dagen of sinds de laatste Hallo-e-mail is verzonden, afhankelijk van wat kleiner is.</span><span class="sxs-lookup"><span data-stu-id="6eec1-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="6eec1-115">Hoe krijg ik toegang tot Hallo rapport die worden vermeld in Hallo e-mailbericht?</span><span class="sxs-lookup"><span data-stu-id="6eec1-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="6eec1-116">Wanneer u op Hallo koppeling klikt, kunt u zich de rapportpagina omgeleide toohello binnen Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6eec1-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="6eec1-117">In volgorde tooaccess rapport hello, moet u beide toobe:</span><span class="sxs-lookup"><span data-stu-id="6eec1-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="6eec1-118">Een beheerder of co-beheerder van uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="6eec1-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="6eec1-119">Een globale beheerder in de directory hello, en een Active Directory Premium-licentie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6eec1-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="6eec1-120">Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6eec1-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="6eec1-121">Kan ik deze e-mailberichten uitschakelen?</span><span class="sxs-lookup"><span data-stu-id="6eec1-121">Can I turn off these emails?</span></span>
<span data-ttu-id="6eec1-122">Ja, tooturn meldingen uit gerelateerde tooanomalous aanmeldingen binnen Hallo klassieke Azure-portal, klikt u op **configureren**, en selecteer vervolgens **uitgeschakelde** onder Hallo **meldingen**sectie.</span><span class="sxs-lookup"><span data-stu-id="6eec1-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="6eec1-123">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="6eec1-123">What's next</span></span>
* <span data-ttu-id="6eec1-124">Meer wilt weten over welke beveiliging, controle en rapporten van activiteiten zijn beschikbaar?</span><span class="sxs-lookup"><span data-stu-id="6eec1-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="6eec1-125">Bekijk [Azure AD-beveiliging, controle en rapporten van activiteiten](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="6eec1-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="6eec1-126">Aan de slag met Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="6eec1-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="6eec1-127">Huisstijl tooyour dat pagina's voor aanmelden en de Toegangsvensterpagina toevoegen</span><span class="sxs-lookup"><span data-stu-id="6eec1-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

