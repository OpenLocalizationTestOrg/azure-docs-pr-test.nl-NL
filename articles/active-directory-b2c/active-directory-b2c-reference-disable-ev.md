---
title: 'Azure Active Directory B2C: E-mailverificatie tijdens registratie Consumer uitschakelen | Microsoft Docs'
description: Een onderwerp laat zien hoe u een e-mailverificatie tijdens registratie in Azure Active Directory B2C consumer uitschakelen
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="f9063-103">Azure Active Directory B2C: Schakel e-mailverificatie tijdens registratie consumer</span><span class="sxs-lookup"><span data-stu-id="f9063-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="f9063-104">Wanneer dit is ingeschakeld, kunt Azure Active Directory (Azure AD) B2C een consument zich aanmelden voor toepassingen door een e-mailadres en een lokaal account maken.</span><span class="sxs-lookup"><span data-stu-id="f9063-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="f9063-105">Azure AD B2C, zorgt u ervoor geldige e-mailadressen doordat consumenten om te controleren of ze tijdens het registratieproces.</span><span class="sxs-lookup"><span data-stu-id="f9063-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="f9063-106">Dit voorkomt ook dat een kwaadwillende geautomatiseerd proces valse accounts voor de toepassingen te genereren.</span><span class="sxs-lookup"><span data-stu-id="f9063-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="f9063-107">Sommige toepassingsontwikkelaars liever overslaan e-mailverificatie tijdens het registratieproces en hebt in plaats daarvan consumenten later controleren van het e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="f9063-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="f9063-108">Ter ondersteuning hiervan, kan Azure AD B2C worden geconfigureerd voor het e-controle niet uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f9063-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="f9063-109">Dit leidt tot een soepeler aanmeldingsproces maakt en biedt ontwikkelaars de flexibiliteit om te onderscheiden van consumenten die hun e-mailadres van consumenten die nog niet hebt geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="f9063-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="f9063-110">Registratie beleidsregels hebben standaard e-mailverificatie ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f9063-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="f9063-111">Gebruik de volgende stappen uit te schakelen:</span><span class="sxs-lookup"><span data-stu-id="f9063-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="f9063-112">[Volg deze stappen om te navigeren naar de blade B2C-functies in de Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="f9063-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="f9063-113">Klik op **aanmelding beleid** of **registreren of aanmelden beleid** afhankelijk van wat u hebt geconfigureerd voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="f9063-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="f9063-114">Klik op het beleid (bijvoorbeeld ' B2C_1_SiUp') om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="f9063-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="f9063-115">Klik op **bewerken** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="f9063-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="f9063-116">Klik op **pagina UI-aanpassing**.</span><span class="sxs-lookup"><span data-stu-id="f9063-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="f9063-117">Klik op **aanmeldpagina voor lokaal account**.</span><span class="sxs-lookup"><span data-stu-id="f9063-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="f9063-118">Klik op **e-mailadres** in de **naam** kolom onder de **registratiekenmerken** sectie.</span><span class="sxs-lookup"><span data-stu-id="f9063-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="f9063-119">Schakelen tussen de **verificatie vereisen** optie naar **Nee**.</span><span class="sxs-lookup"><span data-stu-id="f9063-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="f9063-120">Klik op **OK** onder totdat u de **beleid bewerken** blade.</span><span class="sxs-lookup"><span data-stu-id="f9063-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="f9063-121">Klik op **opslaan** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="f9063-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="f9063-122">U bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="f9063-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="f9063-123">Het uitschakelen van e-mailverificatie in het aanmeldingsproces kan leiden tot spam.</span><span class="sxs-lookup"><span data-stu-id="f9063-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="f9063-124">Als u de standaardtabel uitschakelt, wordt u aangeraden het toevoegen van uw eigen-verificatiesysteem.</span><span class="sxs-lookup"><span data-stu-id="f9063-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="f9063-125">We kunnen worden altijd feedback en suggesties!</span><span class="sxs-lookup"><span data-stu-id="f9063-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="f9063-126">Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zouden we stellen uw feedback onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="f9063-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="f9063-127">Voor functieaanvragen, voeg deze toe aan [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="f9063-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>