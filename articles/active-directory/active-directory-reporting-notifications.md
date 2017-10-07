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
# <a name="azure-active-directory-reporting-notifications"></a>Azure Active Directory-rapportage meldingen
## <a name="what-reports-generate-email-notifications"></a>Welke rapporten genereren e-mailmeldingen
Op dit moment alleen Hallo onregelmatige aanmelding in activiteit rapport triggers e-mailmeldingen.

## <a name="what-is-an-irregular-sign-in"></a>Wat is een 'onregelmatige aanmelden'?
Onregelmatige aanmeldingen zijn bestanden die zijn geïdentificeerd door onze machine learning-algoritmen, op basis van een 'onmogelijke reis' voorwaarde gecombineerd met een afwijkende locatie aanmelden en het apparaat Hallo. Dit kan erop wijzen dat een hacker is probeert toosign in dit account wordt gebruikt.

## <a name="who-receives-hello-email-notifications"></a>Wie Hallo e-mailmeldingen ontvangen?
Hallo-e-mailbericht verzonden tooall globale beheerders die zijn toegewezen in een Active Directory Premium-licentie. tooensure die wordt bezorgd, we verzenden toohello admins alternatief e-mailadres ook. Beheerders moeten bevatten aad-alerts-noreply@mail.windowsazure.com in hun lijst met veilige afzenders zodat er geen Hallo e zijn gemist.

## <a name="how-often-are-these-emails-sent"></a>Hoe vaak worden deze e-mailberichten verzonden?
Hallo-e-mailbericht wordt verzonden als de 10 nieuwe onregelmatige aanmelden activiteiten plaatsvinden in Hallo afgelopen 30 dagen of sinds de laatste Hallo-e-mail is verzonden, afhankelijk van wat kleiner is.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Hoe krijg ik toegang tot Hallo rapport die worden vermeld in Hallo e-mailbericht?
Wanneer u op Hallo koppeling klikt, kunt u zich de rapportpagina omgeleide toohello binnen Hallo klassieke Azure-portal. In volgorde tooaccess rapport hello, moet u beide toobe:

* Een beheerder of co-beheerder van uw Azure-abonnement
* Een globale beheerder in de directory hello, en een Active Directory Premium-licentie toegewezen. Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.

## <a name="can-i-turn-off-these-emails"></a>Kan ik deze e-mailberichten uitschakelen?
Ja, tooturn meldingen uit gerelateerde tooanomalous aanmeldingen binnen Hallo klassieke Azure-portal, klikt u op **configureren**, en selecteer vervolgens **uitgeschakelde** onder Hallo **meldingen**sectie.

## <a name="whats-next"></a>Volgend onderwerp
* Meer wilt weten over welke beveiliging, controle en rapporten van activiteiten zijn beschikbaar? Bekijk [Azure AD-beveiliging, controle en rapporten van activiteiten](active-directory-view-access-usage-reports.md)
* [Aan de slag met Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Huisstijl tooyour dat pagina's voor aanmelden en de Toegangsvensterpagina toevoegen](active-directory-add-company-branding.md)

