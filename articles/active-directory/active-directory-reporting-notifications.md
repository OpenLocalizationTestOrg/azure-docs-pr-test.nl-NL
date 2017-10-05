---
title: Azure Active Directory-rapportage meldingen
description: Het gebruik van de Azure Active Directory-rapportage meldingen voor verdacht modules.
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
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="0bc17-103">Azure Active Directory-rapportage meldingen</span><span class="sxs-lookup"><span data-stu-id="0bc17-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="0bc17-104">Welke rapporten genereren e-mailmeldingen</span><span class="sxs-lookup"><span data-stu-id="0bc17-104">What reports generate email notifications</span></span>
<span data-ttu-id="0bc17-105">Op dit moment de onregelmatige aanmelden activiteit rapport triggers e-mailmeldingen.</span><span class="sxs-lookup"><span data-stu-id="0bc17-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="0bc17-106">Wat is een 'onregelmatige aanmelden'?</span><span class="sxs-lookup"><span data-stu-id="0bc17-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="0bc17-107">Onregelmatige aanmeldingen zijn bestanden die zijn geïdentificeerd door onze machine learning-algoritmen, op basis van een 'onmogelijke reis' voorwaarde gecombineerd met een afwijkende locatie aanmelden en het apparaat.</span><span class="sxs-lookup"><span data-stu-id="0bc17-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="0bc17-108">Dit kan erop wijzen dat een hacker heeft is probeert aan te melden met dit account.</span><span class="sxs-lookup"><span data-stu-id="0bc17-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="0bc17-109">Wie de e-mailmeldingen ontvangen?</span><span class="sxs-lookup"><span data-stu-id="0bc17-109">Who receives the email notifications?</span></span>
<span data-ttu-id="0bc17-110">Het e-mailbericht wordt verzonden naar alle globale beheerders die zijn toegewezen in een Active Directory Premium-licentie.</span><span class="sxs-lookup"><span data-stu-id="0bc17-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="0bc17-111">Deze is geleverd, zodat verzenden we naar de beheerders alternatief e-mailadres ook.</span><span class="sxs-lookup"><span data-stu-id="0bc17-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="0bc17-112">Beheerders moeten bevatten aad-alerts-noreply@mail.windowsazure.com in hun lijst met veilige afzenders zodat ze niet de e-mail niet.</span><span class="sxs-lookup"><span data-stu-id="0bc17-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="0bc17-113">Hoe vaak worden deze e-mailberichten verzonden?</span><span class="sxs-lookup"><span data-stu-id="0bc17-113">How often are these emails sent?</span></span>
<span data-ttu-id="0bc17-114">Het e-mailbericht wordt verzonden als de 10 nieuwe onregelmatige aanmelden activiteiten plaatsvinden in de afgelopen 30 dagen of sinds het laatste e-mailbericht is verzonden, afhankelijk van wat kleiner is.</span><span class="sxs-lookup"><span data-stu-id="0bc17-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="0bc17-115">Hoe krijg ik toegang tot het rapport dat wordt vermeld in het e-mailbericht?</span><span class="sxs-lookup"><span data-stu-id="0bc17-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="0bc17-116">Wanneer u op de koppeling klikt, wordt u omgeleid naar de rapportpagina in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0bc17-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="0bc17-117">Als u het rapport opent, moet u beide:</span><span class="sxs-lookup"><span data-stu-id="0bc17-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="0bc17-118">Een beheerder of co-beheerder van uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="0bc17-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="0bc17-119">Een globale beheerder in de map en een Active Directory Premium-licentie toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0bc17-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="0bc17-120">Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0bc17-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="0bc17-121">Kan ik deze e-mailberichten uitschakelen?</span><span class="sxs-lookup"><span data-stu-id="0bc17-121">Can I turn off these emails?</span></span>
<span data-ttu-id="0bc17-122">Ja, u kunt uitschakelen meldingen betrekking hebben op afwijkende aanmeldingen in de klassieke Azure portal, op **configureren**, en selecteer vervolgens **uitgeschakelde** onder de **meldingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="0bc17-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="0bc17-123">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="0bc17-123">What's next</span></span>
* <span data-ttu-id="0bc17-124">Meer wilt weten over welke beveiliging, controle en rapporten van activiteiten zijn beschikbaar?</span><span class="sxs-lookup"><span data-stu-id="0bc17-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="0bc17-125">Bekijk [Azure AD-beveiliging, controle en rapporten van activiteiten](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="0bc17-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="0bc17-126">Aan de slag met Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="0bc17-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="0bc17-127">De huisstijl van uw bedrijf toevoegen aan de aanmeldingspagina en de toegangsvensterpagina’s</span><span class="sxs-lookup"><span data-stu-id="0bc17-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

