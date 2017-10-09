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
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="84d6a-103">Azure Active Directory B2C: Schakel e-mailverificatie tijdens registratie consumer</span><span class="sxs-lookup"><span data-stu-id="84d6a-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="84d6a-104">Wanneer dit is ingeschakeld, hello Azure Active Directory (Azure AD) B2C biedt een consumer mogelijkheid toosign voor toepassingen door een e-mailadres en een lokaal account maken.</span><span class="sxs-lookup"><span data-stu-id="84d6a-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="84d6a-105">Azure AD B2C doordat consumenten tooverify geldige e-mailadressen zorgt ervoor dat deze tijdens het registratieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="84d6a-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="84d6a-106">Dit voorkomt ook dat een kwaadwillende geautomatiseerd proces genereren valse accounts voor Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="84d6a-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="84d6a-107">Sommige toepassingsontwikkelaars liever tooskip e-mailverificatie tijdens het registratieproces hello en in plaats daarvan hebben gebruikers e-mailadres hello later controleren.</span><span class="sxs-lookup"><span data-stu-id="84d6a-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="84d6a-108">Dit Azure AD B2C kunt toosupport geconfigureerde toodisable e-mailverificatie worden.</span><span class="sxs-lookup"><span data-stu-id="84d6a-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="84d6a-109">Dit leidt tot een soepeler aanmeldingsproces maakt en biedt ontwikkelaars Hallo flexibiliteit toodifferentiate Hallo consumenten die hun e-mailadres van consumenten die nog niet hebt geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="84d6a-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="84d6a-110">Registratie beleidsregels hebben standaard e-mailverificatie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="84d6a-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="84d6a-111">Gebruik Hallo volgende stappen tooturn deze uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="84d6a-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="84d6a-112">[Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="84d6a-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="84d6a-113">Klik op **aanmelding beleid** of **registreren of aanmelden beleid** afhankelijk van wat u hebt geconfigureerd voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="84d6a-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="84d6a-114">Klik op uw tooopen beleid (bijvoorbeeld ' B2C_1_SiUp') deze.</span><span class="sxs-lookup"><span data-stu-id="84d6a-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="84d6a-115">Klik op **bewerken** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="84d6a-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="84d6a-116">Klik op **pagina UI-aanpassing**.</span><span class="sxs-lookup"><span data-stu-id="84d6a-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="84d6a-117">Klik op **aanmeldpagina voor lokaal account**.</span><span class="sxs-lookup"><span data-stu-id="84d6a-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="84d6a-118">Klik op **e-mailadres** in Hallo **naam** kolom onder Hallo **registratiekenmerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="84d6a-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="84d6a-119">Wisselknop Hallo **verificatie vereisen** te optie**Nee**.</span><span class="sxs-lookup"><span data-stu-id="84d6a-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="84d6a-120">Klik op **OK** onderin Hallo totdat u Hallo **beleid bewerken** blade.</span><span class="sxs-lookup"><span data-stu-id="84d6a-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="84d6a-121">Klik op **opslaan** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="84d6a-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="84d6a-122">U bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="84d6a-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="84d6a-123">Het uitschakelen van e-mailverificatie in Hallo aanmeldingsproces kan toospam leiden.</span><span class="sxs-lookup"><span data-stu-id="84d6a-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="84d6a-124">Als u Hallo standaardtabel uitschakelt, wordt u aangeraden het toevoegen van uw eigen-verificatiesysteem.</span><span class="sxs-lookup"><span data-stu-id="84d6a-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="84d6a-125">We zijn altijd open toofeedback en suggesties!</span><span class="sxs-lookup"><span data-stu-id="84d6a-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="84d6a-126">Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zou wij stellen uw feedback Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="84d6a-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="84d6a-127">Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="84d6a-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
