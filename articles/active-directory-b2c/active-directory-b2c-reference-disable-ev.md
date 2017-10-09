---
title: 'Azure Active Directory B2C: E-mailverificatie tijdens registratie Consumer uitschakelen | Microsoft Docs'
description: Een onderwerp te demonstreren hoe toodisable e-verificatie tijdens de registratie in Azure Active Directory B2C consumer
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: Schakel e-mailverificatie tijdens registratie consumer
Wanneer dit is ingeschakeld, hello Azure Active Directory (Azure AD) B2C biedt een consumer mogelijkheid toosign voor toepassingen door een e-mailadres en een lokaal account maken. Azure AD B2C doordat consumenten tooverify geldige e-mailadressen zorgt ervoor dat deze tijdens het registratieproces Hallo. Dit voorkomt ook dat een kwaadwillende geautomatiseerd proces genereren valse accounts voor Hallo toepassingen.

Sommige toepassingsontwikkelaars liever tooskip e-mailverificatie tijdens het registratieproces hello en in plaats daarvan hebben gebruikers e-mailadres hello later controleren. Dit Azure AD B2C kunt toosupport geconfigureerde toodisable e-mailverificatie worden. Dit leidt tot een soepeler aanmeldingsproces maakt en biedt ontwikkelaars Hallo flexibiliteit toodifferentiate Hallo consumenten die hun e-mailadres van consumenten die nog niet hebt geverifieerd.

Registratie beleidsregels hebben standaard e-mailverificatie ingeschakeld. Gebruik Hallo volgende stappen tooturn deze uitschakelen:

1. [Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Klik op **aanmelding beleid** of **registreren of aanmelden beleid** afhankelijk van wat u hebt geconfigureerd voor aanmelding.
3. Klik op uw tooopen beleid (bijvoorbeeld ' B2C_1_SiUp') deze. Klik op **bewerken** Hallo boven aan het Hallo-blade.
4. Klik op **pagina UI-aanpassing**.
5. Klik op **aanmeldpagina voor lokaal account**.
6. Klik op **e-mailadres** in Hallo **naam** kolom onder Hallo **registratiekenmerken** sectie.
7. Wisselknop Hallo **verificatie vereisen** te optie**Nee**.
8. Klik op **OK** onderin Hallo totdat u Hallo **beleid bewerken** blade.
9. Klik op **opslaan** Hallo boven aan het Hallo-blade. U bent nu klaar!

> [!NOTE]
> Het uitschakelen van e-mailverificatie in Hallo aanmeldingsproces kan toospam leiden. Als u Hallo standaardtabel uitschakelt, wordt u aangeraden het toevoegen van uw eigen-verificatiesysteem.
> 
> 

We zijn altijd open toofeedback en suggesties! Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zou wij stellen uw feedback Hallo Hallo pagina onderaan in. Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
